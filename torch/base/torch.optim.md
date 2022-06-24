`torch.optim` 是一个实现了各种优化算法的库。大部分常用的方法得到支持，并且接口具备足够的通用性，使得未来能够集成更加复杂的方法。

为了构建一个`Optimizer`，你需要给它一个包含了需要优化的参数（必须都是`Variable`对象）的iterable。然后，你可以设置optimizer的参 数选项，比如学习率，权重衰减，等等。

```python
optimizer = optim.SGD(model.parameters(), lr = 0.01, momentum=0.9)
optimizer = optim.Adam([var1, var2], lr = 0.0001)
```

