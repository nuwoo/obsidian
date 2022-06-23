返回这个张量的一个新视图，其中

```python
Tensor.expand(*sizes) -> Tensor
```

- `*sizes` (torch size or int) , the desired expanded size.


## demo

```python
x = torch.tensor([[1], [2], [3]])
x.size()  # torch.Size([3, 1])
x.expand(3, 4) 
#tensor([[ 1,  1,  1,  1],
#        [ 2,  2,  2,  2],
#        [ 3,  3,  3,  3]])
x.expand(-1, 4)   # -1 means not changing the size of that dimension
#tensor([[ 1,  1,  1,  1],
#        [ 2,  2,  2,  2],
#        [ 3,  3,  3,  3]])
```

