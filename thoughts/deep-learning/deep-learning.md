# 深度学习框架/语言

我认为一个好的深度学习框架/语言应该具备以下特性：

`broadcast`特性。这点不必说，`PyTorch`和`TensorFlow`都有，`broadcast`是一个很好的特性，可以让我们写出更加简洁的代码。

函数式编程范式。因为深度学习的各种操作本质都是函数，所以使用函数式编程范式可以让我们写出更加简洁的代码。

`named tensor`特性。`named tensor`就是给`shape`加上了名字。比如`PyTorch`的`view`操作，`TensorFlow`的`reshape`操作，这些操作都是不太方便，因为它们都是通过`shape`来操作的。
数字索引的`shape`是一个`int`数组，就像`[32, 100, 200]`。
使用`named tensor`就类似于`{'batch':32, 'time':100, 'hidden':200}`，其使用名称而不是位置来指代轴。
其中`{'batch':32, 'time':100, 'hidden':200}`和`{'time':100, 'hidden':200, 'batch':32}`的`shape`是一样的。

无序的索引。因为使用命名索引而不是数字索引，所以索引不需要顺序。访问某个元素或者是切片时，只需要提供相应的名称即可，而不需要按照顺序提供所有的索引。这有点类似于“命名参数”和“位置参数”的区别。
以上面的例子来说，我们可以这样访问某个元素：`tensor[{'batch':0, 'time':1, 'hidden':2}]`，也可以这样访问：`tensor[{'time':1, 'hidden':2, 'batch':0}]`。

爱因斯坦表示法。拥有类似`einops`的通过名称而不是索引来操作`tensor`的特性，这样可以让我们写出更加简洁的代码。

自动调整轴位置。自动将迭代的轴放在最前面，不需要手动调整轴顺序，只需要指定迭代的轴即可。
例如当使用`for t in tensor['time']`时，框架会自动将底层的`tensor`的轴调整为`time, batch, hidden`。
而我们不需要关心迭代的效率问题，因为框架会自动调整轴的顺序。

```python
# tensor.named_shape={'batch':32, 'time':100, 'hidden':200}

t[{'time':0, 'hidden':0}] = 1000 # Select tensor with axis time 0 and axis hidden 0, and set tensor to 1000 with broadcast.

for t in tensor['time']:
# Jax automatically performs dimension permutation for operations: tensor: batch, time, hidden -> time, batch, hidden
# t.named_shape = {'batch':32, 'hidden':200}
    ...
```
