shared_ptr 是一种智能指针，它的作用和指针类似，但会记录有多少个 shared_ptr 共同指向同一个对象，这便是所谓的引用计数。

当最后一个这样的指针被销毁，也就是说一旦某个对象的引用计数为 0 ，这个对象就会被自动删除。


## 参考

[智能指针——shared_ptr](https://blog.csdn.net/weixin_45732589/article/details/115741770)