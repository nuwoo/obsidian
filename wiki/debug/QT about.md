## Linux QT build without executable file

### Problem

Linux 环境下选择 debug 或是 release 都无法生成可执行文件（application/x-executable)，而是一个 share libary 文件，编译过程无报错。

### Solution

打开 `xxx.pro` 文件，添加如下内容即可：

![https://img-blog.csdnimg.cn/20191030144350673.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3N1bm55d215,size_16,color_FFFFFF,t_70](https://img-blog.csdnimg.cn/20191030144350673.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3N1bm55d215,size_16,color_FFFFFF,t_70)

有时无法运行可能是权限不够，赋予可执行权限即可：

```bash
chmod +x exec_file
./exec_file
```


---

## the code model could not parse an include file

### Problem

即使是刚创建一个 qt project ，在编辑文件件时，也还是提示头文件相关的问题，提示内容为：

```txt
the code model could not parse an include file, which might lead to incorrect code completion and highlighting.
```

### Solution

打开 `help - about plugins - c++` ，将 `ClangCodeMode` 的选项去掉即可，如图所示：

![could-not-parse | 500](https://img-blog.csdnimg.cn/20181225094358231.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTI2ODYxNTQ=,size_16,color_FFFFFF,t_70)

重启 qt creator ，然后问题解决。

