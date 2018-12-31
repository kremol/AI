# Glove 词向量


https://www.fanyeong.com/2018/02/19/glove-in-detail/
这篇文章讲得很好

注意的点：
1. Glove 是一个基于全局词频统计的的方法
2. 做法大致是：
- 构建共现矩阵
- 构建词向量和共现矩阵的关系
- 写出来loss function
- 随机初始化词向量，然后用梯度下降求

3. 因为在选择co-concurrence matrix 的时候，要选一个context word 做中心。所以公式里假定了两套词向量w，这样就训练出来了2个w，这两个w是等价的都能用  
具体地，这篇论文里的实验是这么做的：采用了AdaGrad的梯度下降算法，对矩阵X中的所有非零元素进行随机采样，学习曲率（learning rate）设为0.05，在vector size小于300的情况下迭代了50次，其他大小的vectors上迭代了100次，直至收敛。最终学习得到的是两个vector是w和~w，因为X是对称的（symmetric），所以从原理上讲w和~w是也是对称的，他们唯一的区别是初始化的值不一样，而导致最终的值不一样。所以这两者其实是等价的，都可以当成最终的结果来使用。但是为了提高鲁棒性，我们最终会选择两者之和w+~w作为最终的vector（两者的初始化不同相当于加了不同的随机噪声，所以能提高鲁棒性）。

A practice  
https://medium.com/@japneet121/word-vectorization-using-glove-76919685ee0b