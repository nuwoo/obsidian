## 综述

pip （package installer for python）是一个现代的，通用的 Python 包管理工具。提供了对 Python 包的查找、下载、安装、卸载的功能。pip 最大的优势是它不仅能将我们需要的包下载下来，而且会把相关依赖的包也下载下来。


## 命令及其参数

`pip -help` 查看 pip 命令的参数及其用法

`pip --version` 查看当前 pip 版本，也可以检查当前环境是否存在 pip 

## 常用命令

#### 安装

安装 package 的命令如下，默认安装环境支持的最新包，也可以指定版本。

```bash
pip install <package_name> 
pip istall <package_name=1.2.3
```

批量安装一些包可以使用 requirements.txt 

```bash
pip install -r requirements.txt
```

#### 卸载

```bash
pip uninstall <package>
```

#### 查看 package

查看当前环境下安装的包及其版本

```bash
pip freeze
```

#### 升级包

```bash
pip list -o # 可升级的包
pip install -U <package> # 安装指定的包
```

### 升级 pip

升级 pip 有时会遇到问题，大部分情况都可以用如下命令解决：

```bash
python -m pip install --upgrade pip
```

### 下载 package 到本地

将 package 下载到本地时可供其他平台使用，文件格式为 `.whl` 。

```bash
pip download package_name -d "save_path"
```

## 更换 pip 源

鉴于国内的网络环境，使用 pip 安装有时会很慢，需要换源

### 临时使用

```bash
pip install <packages> -i https://pypi.tuna.tsinghua.edu.cn/simple # 清华源
pip install <packages> -i https://pypi.douban.com/simple # 豆瓣源
pip install <packages> -i https://pypi.mirrors.ustc.edu.cn/simple/ # 中科大源
```

### 永久替换

