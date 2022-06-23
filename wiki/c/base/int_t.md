int_t 为一个结构的标注，可以理解为 type/typedef 的缩写，表示它是通过 typedef 定义的，而不是一种新的数据类型。

因为跨平台，不同的平台会有不同的字长，所以利用[预编译](https://so.csdn.net/so/search?q=%E9%A2%84%E7%BC%96%E8%AF%91&spm=1001.2101.3001.7020)和 typedef 可以最有效的维护代码。

int8_t : typedef signed char;
uint8_t : typedef unsigned char;
int16_t : typedef signed short ;
uint16_t : typedef unsigned short ;
int32_t : typedef signed int;
uint32_t : typedef unsigned int;
int64_t : typedef signed long long;
uint64_t : typedef unsigned long long;

### size_t 与 ssize_t 

在不同系统上，`size_t` 的定义不同。他的大小和系统的位数有关。它是用来表示一个结构或一个数据占据多少字节的一个单位。

-   32位系统上，`size_t` 是 `unsigned int`，是32位无符号整型。占个4字节；
-   64位系统上，`size_t` 是 `unsigned long` ，是64位无符号整型，占8个字节。

`ssize_t` 是有符号整型，在 32 位机器上等同 int ，在 64 位机器上等同 long int 。

