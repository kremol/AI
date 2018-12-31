# gensim 的doc2vec的用法
要把文档split成词，然后每个文档分一个tag  
之后构建model = Doc2Vec(...)  
然后train就可以了，注意train的时候要shuffle  
其他的看官方的doc2vec_tutorial和API即可  
文件夹里是tutorial的代码和一个情感分析的例子。发现的trick在注释上  