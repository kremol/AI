# Tensorflow 的坑

1. 
- sparse_softmax_cross_entropy_with_logits函数，logits是预测的，labels是真实的标签。labels传tf.argmax(y,1)  
- 而softmax_cross_entropy_with_logits 的labels要传y，这两个刚好相反  
- 同时logits要传没有做过softmax的矩阵/向量，否则在函数里还会再做一次softmax  
- 如果是矩阵的话，最后再tf.reduce_sum得到总的损失