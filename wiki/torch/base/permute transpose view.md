r## permute

permute 主要将 tensor 的维度进行变换

```python
torch.Tensor.permute (Python method, in torch.Tensor)
```

- dims, 矩阵的维度，一维就是 0，二维就是 0,1 

## demo

```python
>>> x = torch.randn(2,3,5)
>>> x.ize()
torch.Size([2,3,5])
>>> x.permute(2,0,1).size()
torch.Size([5,2,3]) 
```


## transpose

```python
torch.transpose(x, a, b)
```

transpose 仅能进行二维转换，即将 a b 两个维度的数据进行交换。

## view

view 的作用和 numpy 中的 reshape 一致，相当于重新定义矩阵的形状。

### demo

```python
import torch
v1.torch.range(1,16)
v2 = v1.view(4,4)
```

v1 为 1\*16 的张量，包含 16 个元素；v2 为 大小 4 \*  4 的张量，元素个数相同。

```python
import torch
v1.torch.range(1.16)
v2 = v1.view(-1,4)
```

第一个参数设定为 -1 ，表示动态调整此维度上的元素个数，保证总元素个数不变。

## contiguous

```python
tensor.contiguous(memory_format=torch.contiguous_format) -> tensor
```

Returns a contiguous in memory tensor containing the same data as self tensor. If self tensor is already in the specified memory format, this function returns the self tensor.

contiguous 一般和 [view](#view) 一起使用，tensor.view 方法对张量形状的改变并没改变张量在内存中真正的形状，而是重新定义了访问张量的规则，内存中的张量还是和原来一样。

### demo

pytorch 和 numpy 在存储 M \times N 的数组时，都是一维的形式，对于一个二维张量 t 

```python
t = torch.tensor([[2, 1, 3], [4, 5, 9]])
```

内存中的形式是

```python
[2, 1, 3, 4, 5, 9]
```

当使用 torch.transpose() 或是 torch.permute() 对张量进行翻转后，改变了 tensor 的形状。

```python
t2 = t.transpose(0,1)
t2
```

```text
tensor([[2,4], 
		[1,5], 
		[3,9])
```

此时对 t2 进行 view 就会报错，原因是 t2 逻辑上是 3 行 2 列的，内存上和 t 一致，按照逻辑上的形式进行 view ，数字不连续，此时使用 contiuous 方法。

## 参考

[torch.contiguos()方法](https://blog.csdn.net/qq_37828380/article/details/107855070?spm=1001.2101.3001.6650.4&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-4-107855070-blog-80143212.pc_relevant_antiscanv2&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-4-107855070-blog-80143212.pc_relevant_antiscanv2&utm_relevant_index=7)