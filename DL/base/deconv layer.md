## 卷积



## 反卷积

反卷积和转置卷积是同一个概念，反卷积，就是卷积的逆操作，如果将上图的卷积看成是输入通过卷积核的透视，那么反卷积就可以看成输出通过卷积核的透视，如下图所示：

![deconv | 500](additions/deconv-1.png)

将得到的四张特征图进行叠加，叠加的方式同样和卷积类似，featuremap 之间滑动叠加，重合部分值想加，得到如下结果：

![deconv-2 | 500](additions/deconv-2.png)

得到的 featuremap 和 输入的 featuremap 大小相同，但是值不同，说明卷积和反卷积并不是可逆的操作，**反卷积只能恢复尺寸，不能恢复信息** 。

## 反卷积和转置卷积

反卷积就是将卷积操作中的卷积核矩阵进行了转置，所以反卷积也称为转置卷积。

