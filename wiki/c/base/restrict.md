 restrict 是 c99 标准引入的，它只可以用于限定和[约束](https://so.csdn.net/so/search?q=%E7%BA%A6%E6%9D%9F&spm=1001.2101.3001.7020)指针，并表明指针是访问一个数据对象的唯一且初始的方式。
 
 它告诉编译器，所有修改该指针所指向内存中内容的操作都必须通过该指针来修改,而不能通过其它途径(其它变量或指针)来修改;
 
 这样做的好处是,能帮助编译器进行更好的优化代码,生成更有效率的汇编代码。
 