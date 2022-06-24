通过 torch.optim.lr_scheduler 接口实现，torch 提供三种调整策略：

- 有序调整
- 自适应调整
- 自定义调整

## stepLR

等间隔调整学习率，调整倍数为 gamma ，调整间隔为 step_size ，随着 epochs 的变化，学习率也不断调整。

```python
torch.optim.lr_scheduler.StepLR(optimizer, step_size, gamma=0.1, last_epoch=-1)
```

- `step_size` ，学习率下降间隔数，如为 30 ，则会在epochs为 30、60、90时，将学习率调整为 `lr*gamma` 。
- `gamma` ，学习率调整倍数，默认为 0.1 ，也就是下降 10 倍。
- `last_epoch` ，上一个 epoch 数，当符合设定的间隔时，就会对学习率进行调整。

