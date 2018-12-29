# Word2vec

- 两种模型CBOW(context words预测一个word) 和 Skip-gram（一个word预测context）

- 结构其实是，输入层，W，隐层，W’，输出层，softmax，最终层

- 注意CBOW这种模型中多个输入是共用一个W的，因此，对输入向量平均，也就相当于让每个输入都乘以W后得到h，然后对所有的h平均。同理skip-gram，隐层到输出层的W’是多个输出向量共用的。

- 损失函数用的是max某一个单词的概率。如果是skip-gram模型，就max所有单词

- hierarchical softmax 是加速训练的方法。它替换掉了原先的隐层到输出层这一大块(原先的W’矩阵，然后再softmax)，变成了一个哈弗曼树。隐层到输出层的训练参数复杂度由O(V)降低到了O(logV),V是vocabulary的大小

- negative sample 也是一种加速训练的过程。原本softmax分母是对所有单词求和得到的，现在我们定义一个所有单词的分布P，从分布P里采样一些单词，然后分母就只加这些单词。



# Doc2vec

- doc2vecy也分两种,PV-DM(多对一),PV-DBOW(一对多)。word vector 是所有 document共用的，每个document独自一个paragraph vector。

- 在word2vec的基础上，PV-DM的输入向量又多加了一个one-hot的paragraph vector。对每一个document都用滑动窗口来得到一些句子，这些句子就是训练样本。每个document的paragraph vector 相同。最后就会训练出所有document的向量，当然，和word2vec一样也是保存在input->hidden layer的矩阵D中的。做预测的时候，也是像训练的时候一样，找一些句子，并且要保持网络的参数不变。只是换了一个新的one-hot的paragraph vector作为输入，**然后矩阵D加一列随机向量**。保持网络其他参数不变，只需要梯度下降求新加的这一列的即可。

- 所以一定要记住，不管是doc2vec还是word2vec，最终得到的word vector 或者paragraph vector 的维数都是和隐层一样的，是可以自己设定的。

- 而PV-DBOW则是给一个paragraph vector，然后预测该文档里一个窗口中的一个单词(随机抽的窗口和单词)这样不断地训练。预测新的时候，就是保持网络参数不变，去梯度下降输入的paragraph vector，来得到新文档的这个paragraph vector。原先文档的paragraph vector就在input->hidden layer 的那个矩阵中。

- doc2vec的motivation原文：The inspirationis that the word vectors are asked to contribute to a prediction task about the next word in the sentence. So despitethe fact that the word vectors are initialized randomly, they can eventually capture semantics as an indirect result of the prediction task. We will use this idea in our paragraph vec-tors in a similar manner. The paragraph vectors are also asked to contribute to the prediction task of the next word given many contexts sampled from the paragraph.  
在word2vec里，即使word vectors是随便初始化的(one-hot)，最终都可以变成含有语义信息的向量。因此，我也可以随便初始化一个paragraph vector，然后来用该document中的句子训练，最终就可以得到能表示文档语义信息或者主题的vector