## TP TN FP FN

T (True) 和 F (False) 代表该样本是否被正确分类，P (positive) 和 N (Negative) 代表样本被分类为什么。

TP ，True Positive ，被分为正样本，分类正确。
FP ，False Positive ，被分为负样本，但分类错误。

## Percesion & Recall



### percesion

Percesion ，精度，定义为分类器认为是正类且确实是正类的部分占所有分类器认为是正类的比例，衡量的是一个分类器分类出来的正类的确是正类的概率。

$$\text{Percesion} = \frac{TP}{TP+FP}$$

仅仅精度不足以衡量分类器的好坏，50个负样本，50个正样本，分类器把49个正样本和50个负样本都分为负样本，1个正样本分为正样本，这样精度也是100%。

### recall

Recall ，召回率，定义为分类器认为是正类并且确实是正类的部分占所有确实是正类的比例，衡量的是一个分类能把所有的正类都找出来的能力。

两种极端情况，如果召回率是100%，就代表所有的正类都被分类器分为正类。如果召回率是0%，就代表没一个正类被分为正类。

## AP

AP ，Average Percesion ，平均精确度，是计算某一类 P-R 曲线下的面积，mAP 则是计算所有类别 P-R 曲线下面积的平均值。

## mAP

mAP ，mean Average Percesion ，平均精确度，定义为所有类别的平均精确度。

## P-R 曲线

P-R 曲线也就是 P 和 R 的关系曲线图，代表召回率和准确率之间的关系，可以在坐标系上做 Percesion 和 recall 的二维曲线。

## ACC

ACC 代表 Accuracy ，准确率，表示预测样本中预测准确数占所有样本数的比例，即

$$ACC = \frac{TP+TN}{TP+FP+TN+FN}$$

## MACs

MACs ，每秒执行的定点乘积累加操作次数的缩写，它是衡量计算机定点处理能力的量，MAC ，Multiple Accumulate  ，乘积累加运算。GMACs ，每秒10亿次的定点乘积累加运算。

