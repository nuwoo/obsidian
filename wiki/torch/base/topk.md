沿着指定的 dim ，返回 input 的 k 个最大元素，dim 没有指定时，默认为 input 的最后一个维度。

```python
torch.topk(input, k, dim=None, largest=True, sorted=True, out=None) -> (Tensor, LongTensor)
```

函数的返回结果是 (vales, indices) 的具名元祖，其中 indices 是返回的 k 个元素在原张量中的索引值。


