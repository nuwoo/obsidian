`assert` 宏定义在 **assert.h** 中，作用是如果它的条件返回错误，则终止程序执行

```c
void assert(int expression)
```

assert 计算 expression ，值为假则先向 stderr 打印一条错误信息，然后调用 abort 来终止程序运行。频繁调用 assert 会极大的影响程序的性能，增加额外的开销。

```c
#include <assert.h>
#include <stdio.h>
#include <stdlib.h>
struct ITEM {
  int key;
  int value;
};
 
/* add item to list, make sure list is not null */
void additem(struct ITEM *itemptr) {
  assert(itemptr != NULL);
  /* add item to list */
}
 
int main(void)
{
  additem(NULL);
  return 0;
}
```