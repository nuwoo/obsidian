`__file__` 变量给出当前 .py 文件的位置，常用的方式是结合 os.path.dirname() 得到py文件的目录绝对路径，从而构造出同目录下另一文件的绝对路径。

```python
import os

basedir = os.path.abspath(os.path.dirname(__file__))
path_another = (os.path.join(basedir, 'another'))
```

