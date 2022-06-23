## Describe

设置 cpu 生成随机数的种子，确保每次运行.py文件时，生成的随机数都是固定的，方便下次复现实验结果。

```python
torch.manual_seed(seed)
```

### paramaters

- seed (int) ，CPU生成随机数的种子。取值范围为`[-0x8000000000000000, 0xffffffffffffffff]`。

### return 

返回一个 torch.Generator 对象。


## demo



