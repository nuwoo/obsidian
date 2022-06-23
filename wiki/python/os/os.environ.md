## describe

通过 os.environ 来获取环境变量，os.environ 是一个字典，通过 `os.environ.get('HOME')` 就可以获得环境变量 HOME 的值，如果存在这个值。

## demo

在多卡平台上设置在某个显卡上运行，采用 CUDA 环境变量 CUDA_VISIBLE_DEVICES 来限定使用。

```python
import os
os.environ['CUDA_VISIBLE_DEVICES'] = opt.gpus_str
```


## 参考

- [CUDA_VISIBLE_DEVICES来限定CUDA程序所能使用的GPU](https://zhuanlan.zhihu.com/p/157295475)
- [设置CUDA_VISIBLE_DEVICES的方法](https://blog.csdn.net/B_DATA_NUIST/article/details/107973053)