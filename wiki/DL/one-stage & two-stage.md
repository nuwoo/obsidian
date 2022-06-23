目前绝大多数的目标检测网络都充分利用了深度学习网络作为骨干网络用来提取图形特征进行分类和定位。

检测器通常分为两类，一类是 two-stage 检测器，具有代表性的是 faster R-CNN ；另一类是 one-stage 检测器，如 YOLO ，SSD 等，two-stage 检测器具有高定位和识别准确性，one-stage 则有速度上的优势。

结构上 two-stage 有一个生成 region proposal 的步骤，然后对其进行预测和分类，one-stage 则是直接对预测框进行回归和分类预测。

