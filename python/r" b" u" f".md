## r" "

`r""` 作用是去除转义字符，如果字符串中存在 `\n` ，则最终结果不是换行符，而是单纯的 `\n` ，如下所示：

```python
str1 = 'input\n'
str2 = r'input\n'
print(str1)
print(str2)
```

输出的结果为 

```txt
input
input\n
```

## u" "

字符串以 Unicode 格式进行编码，一般用在中文字符前，防止出现乱码。

