# Pytorch
## chapter 2 快速入门

- Tensor和numpy对象共享内存，所以他们之间的转换很快，而且几乎不会消耗什么资源。但这也意味着，如果其中一个变了，另外一个也会随之改变

- b.add_(1) # 以`_`结尾的函数会修改自身

- 如果你想获取某一个元素的值，可以使用scalar.item。 直接tensor[idx]得到的还是一个tensor: 一个0-dim 的tensor，一般称为scalar.

- 需要注意的是，t.tensor()总是会进行数据拷贝，新tensor和原来的数据不再共享内存。所以如果你想共享内存的话，建议使用torch.from_numpy()或者tensor.detach()来新建一个tensor, 二者共享内存。
