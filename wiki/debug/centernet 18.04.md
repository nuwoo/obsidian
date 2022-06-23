## 前言

Centernt 推荐的环境是 16.04 + pytorch 0.4.1 + CUDA 0.9.0 等，按照官方文档在 18.04 环境上安装就会出现一系列问题，

### CUDA & CUDNN

CUDA 的版本不是很重要，但是需要与 GPU driver 的版本相符，可以查看 GPU Driver 的版本

#### GPU Driver

查看服务器显卡驱动，如图所示，右上角为 CUDA 支持的最高版本，如果显示其他信息，则显卡驱动存在问题，可以重新安装显卡驱动，显示无误则可以安装 CUDA 了。

```
nvidia-smi
```

![](nvidia-smi.png)

#### CUDA

按照前可以先检查当前环境下是否已经存在 cuda ，通过检查 nvcc 来实现。

```bash
nvcc -V
```

根据机器的 GPU Driver 到官网选择对应的版本后，会出现如图界面，按照提示下载安装即可，推荐 runfile 文件，其余的 installer type 需要较好的网络条件。

![cuda download | 900](additions/cuda_download.png)

> 如需自定义安装路径，需要在 **options** 选项中进行修改，路径为绝对路径。安装完成后在 `.bashrc` 中导入环境变量，修改后 `source ~/.bashrc` 即可。

```bash
export PATH="/media/hy/AI/cuda-11.4/bin:$PATH"
export LD_LIBRARY_PATH="/media/hy/AI/cuda-11.4/lib64:$LD_LIBRARY_PATH"
```

安装完成后可以简单的验证一下，命令行输入 `nvcc -V` ，如果返回版本及其他信息则安装成功。

#### CUDNN

安装 cudnn 有很多方法，网上多推荐 deb 安装，本人选择 deb 没有成功，而是用 tgz 文件安装成功了。cuda 的版本应该与 CUDNN 相同，在[官网](https://docs.nvidia.com/deeplearning/cudnn/support-matrix/index.html)上可以查看，这里选择 CUDA 11.4，对应的 cuDNN 选择 8.4 版本。

![cudnn-download | 700](additions/cudnn-download.png)

解压缩 tgz 会得到一个 cuda 文件夹，然后将一些文件拷贝到 cuda 文件夹下，赋予相关权限，至此 cuda 和 cudnn 安装完成。

```bash
tar -xzvf cudnn_xxx.tgz
sudo cp cuda/include/cudnn.h    /usr/local/cuda-11.3/include
sudo cp cuda/lib64/libcudnn*    /usr/local/cuda-11.3/lib64
sudo chmod a+r /usr/local/cuda-11.3/include/cudnn.h   /usr/local/cuda-11.3/lib64/libcudnn*
```

### conda control editions

单独创建一个虚拟环境来使用 centernet ，python 版本选择 3.6 。

```bash
conda create -n centernrt python=3.6
conda activate centernet
```

### pytorch 1.7

官方文档使用 torch 0.4.1 ，这里改用 torch 1.7.0 ，网上绝大多数方法选择 conda 来安装，但存在一些问题，速度很慢，最后还会有问题。选择 pip 安装很快还没问题。

```bash
pip install torch=1.7.1 torchaduio=0.4.0 torchvision=0.8.0 -i https://pypi.douban.com/simple
```

### clone centernet

 基本环境配置完成后，下载 centernet，使用 pip 批量安装环境要求，同样的可以对 pip 换源。

```bash
git clone https://github.com/xingyizhou/CenterNet
cd CenterNet
pip install -r requirements.txt
```

### DCNv2

绝大多数错误发生在此处，从 demo 到 main ，官方环境下的 DCNv2 版本适用于 torch 0.4 ，需要下载最新的 DCNv2 进行替换，替换路径为 `Centernet/src/lib/models/networks` ，然后执行命令

```bash
cd CenterNet/src/lib/models/networks/DCNv2
python setup.py build develop 
```

### NMS

编译 NMS 可以多尺度的测试 ExtremeNet 。

```bash
cd CenterNet/src/lib/external
make
```

### demo 测试

测试 demo 前需要提前[下载](https://jiangyang.lanzouf.com/b00vk7k9i)模型文件（密码eixi），将模型放置在 models 文件夹下。

```bash
python main.py ctdet --exp_id coco_dla --batch_size 32 --master_batch 15 --lr 1.25e-4  --gpus 0
```

## 训练数据

demo 测试验证无误后可以尝试自己训练数据，根据官方给出的 GET_STARTED 文档进行，同样的使用 coco 数据集来实现，在


## onnx

在实现 pth 转 onnx 的过程中发现不支持 DCNv2 模块，尝试了很多方法，最后只能切换 backbone 类型为 Res18 ，在 demo 文件下进行转换，成功得到 onnx 文件。

```python
from __future__ import absolute_import
from __future__ import division
from __future__ import print_function

import _init_paths
import torch
import os
import cv2
import sys
from opts import opts
from detectors.detector_factory import detector_factory

sys.path.append('/home/dhx/hy/model/CenterNet-master/src')
image_ext = ['jpg', 'jpeg', 'png', 'webp']
video_ext = ['mp4', 'mov', 'avi', 'mkv']
time_stats = ['tot', 'load', 'pre', 'net', 'dec', 'post', 'merge']

def demo(opt):
    os.environ['CUDA_VISIBLE_DEVICES'] = opt.gpus_str
    opt.debug = max(opt.debug, 1)
    Detector = detector_factory[opt.task]
    detector = Detector(opt)
    #print('===============>',detector.model)

    imgsz = (512, 512)
    # # Eval mode
    # model.to(opt.device).eval()
    # # Fuse Conv2d + BatchNorm2d layers
    # # Export mode
    # #model.fuse()
    img = torch.zeros((1, 3) + imgsz)  # (1, 3, 512, 512)
    img = img.to(opt.device)
    # #f = opt.weights.replace(opt.weights.split('.')[-1], 'onnx')  # *.onnx filename
    f = 'car_keypoint.onnx'
    torch.onnx.export(detector.model, img, f, verbose=True, opset_version=9,
                       input_names=['images'], output_names=['hm', 'wh', 'hps', 'reg', 'hm_hp', 'hp_offset'],dynamic_axes=None)
    #
    # # Validate exported model
    # import onnx
    # model = onnx.load(f)  # Load the ONNX model
    # onnx.checker.check_model(model)  # Check that the IR is well formed
    # print(onnx.helper.printable_graph(model.graph))  # Print a human readable representation of the graph
    # return

if __name__ == '__main__':
  opt = opts().init()
  demo(opt)
```

