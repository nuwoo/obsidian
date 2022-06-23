## 简介

### 空白和注释

注释以 `/*` 开始，`*/` 结束，但是注释不能嵌套，也就是说 `/*` 和 `*/` 之间的所有内容都被视为注释，无论其中存在多少注释符。

这样就存在一个问题，有时在程序首尾添加注释符并不能保证代码不起作用，这时可采用 `#if` 指令解决。

```c
#if 0
	statements
#endif
```

`#if` 和 `#endif` 之间的程序段在逻辑上就不会被运行，即使其中存在多个注释。

### 预处理指令

```c
#include <stdio.h>
#define MAX_COLS 20
```

以上都是预处理指令（preprocessor directives），它们都是由预处理器（preprocessor）解释的，预处理器读入源代码，根据预处理指令进行修改，然后将修改后的

## 问题

## 练习 - P16

### 1 Hello world

```c
#include<stdio.h>

void main(){
	printf("Hello World!");
}
```

## 2. read and print

```c
#include <stdio.h>

int main(){
    int inputs[MAX_LEN];
    int line = 0;
    int ch = 1;
    while(1){
        int print_line_num = 1;
        while ((ch = getchar()) != EOF && ch != '\\n') {
            if(print_line_num) {
                printf("%d: ",line);
                print_line_num = 0;
            }
            putchar(ch);
        }
        if(ch == EOF) break;
        putchar('\\n');
        line++;
    }
}

// ctrl + D to immitate the EOF
```

## 3 Checks sum

注意读题，输入为 `Hello world!` ，包含换行符，不含换行符是 92 ，换行符的 ASCII 码正好是 10 。（其实理论上来说，按照 1.8.2 的逻辑，可以去掉换行符的检测。。。）

```c
#include <stdio.h>

int main(){
    char checksum = -1;
    int ch = 0;

    while(1){
        while((ch = getchar()) != EOF){
            checksum += ch;
            putchar(ch);
            if(ch == '\\n') break;
        }
        if(ch == EOF) break;
        printf("%d\\n",checksum);
        checksum = -1;
    }
    return 0;
}
```

### 参考

[ASCII码表,ASCII码一览表,ASCII码对照表完整版-ASCII码中文站](https://www.habaijian.com/)