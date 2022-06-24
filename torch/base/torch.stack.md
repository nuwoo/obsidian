沿着一个新维度对输入张量序列进行连接，序列中所有张量形状相同，如将多个2维的张量凑成一个3维的张量，也就是增加新的维度进行堆叠。

```python
outputs = torch.stack(inputs, dim=?) → Tensor`
```

- inputs ，待连接的张量序列
- dim ，新的维度，必须介于 0 ~ len(outputs) 之间

> Python 中的序列数据只有 list 和 tuple 。


## demo


