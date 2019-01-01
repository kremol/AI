# Fasttext

1. Fasttext和CBOW的结构类似，引入了词的形态学特征，即不在用词向量，而是用n-gram向量。词向量就是其n-gram向量相加然后平均

2. 所以fasttext做文档分类的做法就是，对n-gram向量做one-hot编码，然后叠加成一个词向量。之后同CBOW，把一系列词向量给到隐层，隐层再做hierarchical softmax去最大化该文档类的概率

3. 这样，和word2vec一样输入层到隐层的参数矩阵就是训练好的词向量

4. 总结一下，fasttext是做文本分类用的，同时可以得到word embedding。和CBOW的区别就是CBOW把词做ont-hot编码，而fasttext把n-gram做one-hot编码，这样就引入了词的形态学特征。