```python
torch.randint(low=0, high, size, *, generator=None, 
			  out=None, dtype=None, layout=torch.strided, 
			  device=None, requires_grad=False) → Tensor
```

返回一个填充了随机整数的张量，这些整数在 low 和 high 之间均匀生成，张量的 shape 由变量参数 size 来定义。




## demo

```python
a = torch.randint(100, size(1,10000))
```

