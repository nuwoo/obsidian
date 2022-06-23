设置 `torch.backends.cudnn.benchmark=True` 将会让程序在开始时花费一点额外时间，为整个网络的每个卷积层搜索最适合它的卷积实现算法，进而实现网络的加速。

适用场景是网络结构固定（不是动态变化的），网络的输入形状（包括 batch size，图片大小，输入的通道）是不变的，其实也就是一般情况下都比较适用。

设置这个 flag 为 True，我们就可以在 PyTorch 中对模型里的卷积层进行预先的优化，也就是在每一个卷积层中测试 cuDNN 提供的所有卷积实现算法，然后选择最快的那个。这样在模型启动的时候，只要额外多花一点点预处理时间，就可以较大幅度地减少训练时间。

## 参考

-  [巧用PyTorch中的torch.backends.cudnn.benchmark减少训练时间](https://blog.csdn.net/xiasli123/article/details/102645816?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522160722028819215668819190%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=160722028819215668819190&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_click~default-1-102645816.nonecase&utm_term=torch.backends.cudnn&spm=1018.2118.3001.4449)