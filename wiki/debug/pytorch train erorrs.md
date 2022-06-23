## Runtime error: cuDNN error:CUDNN_STATUS_ERROR

batch_size 、图片尺寸过大等，导致显存不足，适当的调小 batch_size 可以解决问题。

CUDA 和 CUDNN 安装失败，但是在训练模型前一般会测试一下环境是否安装成功，同时使用 `nvcc -V` 就可以判断 cuda 是否安装成功。

nvidia 显卡驱动存在问题，重新安装显卡驱动。

## /dev/sdb5 clear:xxx files xxx blocks

使用 Centernet 模型训练 Kitti 数据集，解决完数据集格式、训练参数问题后，又出现[[pytorch train erorrs#Runtime error cuDNN error CUDNN_STATUS_ERROR]] 等问题，当设置 batch_size = 4 后，没有了上述错误，但是系统直接死机了，然后屏幕显示

![creat-model | 600](additions/Screenshot%20from%202022-04-22%2015-12-23.png)

没办法，不懂只能重启，要命的是我不知道问题出在哪里，只能继续减小 batch_size ，结果好了，系统启动不了了。。。

![unnormal-restart | 600](additions/share.jpg)

然后问题演变成 了解决 [[you are in emergency mode]]问题，这个问题之前确实没遇到过，这里解决了很长时间。



