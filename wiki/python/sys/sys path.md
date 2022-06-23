sys.path 特指模块的查询路径的**列表**，初始化是从[环境变量](https://so.csdn.net/so/search?q=%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F&spm=1001.2101.3001.7020)PYTHONPATH。



## demo

在实际使用中，sys.path 可能查询很慢或是查询不到使用的 path ，sys.path 实际上是一个列表，通过 insert 就可以优先检索 path 。

```python
def add_path(path):
	if path not in sys.path:
		sys.path.insert(0, path)
```

