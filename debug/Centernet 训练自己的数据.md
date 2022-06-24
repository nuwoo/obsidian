
## 数据转换

如果数据集格式为 VOC ，需要进行转换，转换脚本如下，转换前保证图片和 xml 文件名一一对应，使用时仅修改 `args`  对应的图片路径参数即可。

## 开始训练

这里以 8 个 class 的数据为例，选取的 task 为 multi_pose ，multi_pose 本身是用来检测人体姿态，当前任务秀下对其进行一些修改：

在 `src/lib/datasets/dataset/` 路径下新建一个 `coco_hp.py` ，文件内容复制 `coco.py` 的内容，然后修改如下：

`class name` 自定义，`num_classes` 修改为数据集分类的数量，`num_joints` 结合实际检测任务更改，`default_resolution`  根据任务需要进行更改。

```python
# lines:13-16
class COCOHP(data.Dataset):
  num_classes = 10 
  num_joints = 4   
  default_resolution = [512, 512]  
```

`mean` 和 `std` 改为根据数据集图像计算得到的结果，也可以不修改

```python
# 17 行 
  mean = np.array([0.40789654, 0.44719302, 0.47026115],
                   dtype=np.float32).reshape(1, 1, 3)
  std  = np.array([0.28863828, 0.27408164, 0.27809835],
                   dtype=np.float32).reshape(1, 1, 3)
```

23 行，将 `super(coco, self)` 改为定义的类名；25 行，根据 img，train， val 的实际路径进行修改 。

```python
  # 23 行
  super(COCOHP, self).__init__() 

  # 25 行
  self.img_dir = "/mnt/data1/1dataset/Centernet/train/image"
  if split == 'val': self.annot_path ="/mnt/data1/1dataset/Centernet/val/fish2808.json"
  else:
      self.annot_path = "/mnt/data1/1dataset/Centernet/train/fish35418.json"
```

修改  `src/lib/opts.py`  

```python
	# 15 行
    self.parser.add_argument('--dataset', default='coco_hp',
                    help='coco | kitti | coco_hp | pascal')
```

backbone 可以进行替换，如 res18 ，dlav0_34 等

```python
 # 61 行

 # model
    self.parser.add_argument('--arch', default='res_18',
                             help='model architecture. Currently tested' 'res_18 | res_101 | resdcn_18 | resdcn_101 | dlav0_34 | dla_34 | hourglass| reg_800 | resfpndcn_34 | hrnet_18')
```

训练模型的各种超参数可以适当修改，如 `batch_size` 结合实际机器的显存修改。

```python
	# 82 行
	
    # train
    self.parser.add_argument('--lr', type=float, default=1.25e-4, 
                    help='learning rate for batch size 32.')
    self.parser.add_argument('--lr_step', type=str,default='30,60,80',
                             help='drop learning rate by 10.')
    self.parser.add_argument('--num_epochs', type=int, default=20,
                             help='total training epochs.')
    self.parser.add_argument('--batch_size', type=int, default=16,
                             help='batch size')
    self.parser.add_argument('--master_batch_size', type=int, default=-1,
                             help='batch size on the master gpu.')
```

hps 的值修改为 `num_joints`  $\times 2$ ，`hm_hp`  改为 `num_joints` 的值

```python
# 321 行
elif opt.task == 'multi_pose':
      opt.flip_idx = dataset.flip_idx
      opt.heads = {'hm': opt.num_classes, 'wh': 2, 'hps': 8}
      if opt.reg_offset:
        opt.heads.update({'reg': 2})
      if opt.hm_hp:
        opt.heads.update({'hm_hp': 4})  #17
```

num_classess 改为当前数据集的类别，dataset 改为前文自定义的 dataset 名称 ，default resolution 可以适当修改。

```python
	# 344 行
	'multi_pose': {
        'default_resolution': [512, 512], 'num_classes':8,
        'mean': [0.408, 0.447, 0.470], 'std': [0.289, 0.274, 0.278],
        'dataset': 'coco_hp', 'num_joints': 4,
        'flip_idx': [[0, 1], [2, 3]]},
```

修改 `src/lib/utils/debugger.py` ，按照当前数据集的定义类别进行设置。

```python
if dataset == 'coco_hp':
      self.names = ['car', "person", "truck", "bus", "cyclist", "conebarrel", 'noparking', 'parking']
      self.num_class = 8  # 17
      self.num_joints = 4
```

