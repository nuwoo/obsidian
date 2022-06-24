## Q1: loading parameter differ from pretrained

```txt
Skip loading parameter hm.2.weight, required shapetorch.Size([10, 64, 1, 1]), loaded shapetorch.Size([2, 64, 1, 1]). If you see this, your model does not fully load the pre-trained weight. Please make sure you have correctly specified --arch xxx or set the correct --num_classes for your own dataset.
```

加载的模型与预训练模型不一致，实际并不影响最后的结果。



