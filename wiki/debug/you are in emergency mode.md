![You-are-in-emergency-mode | 600](additions/share%201.jpg)

出现这种问题的情况很多，上一步操作太卡，电脑开机重启，进入了紧急模式。

## 1. 

**按 entern 键进入命令行！！！**，然后按照提示输入 journalctl -xb ，然后会显示很多日志，enter 会翻页查看，只需要定位问题所在即可，输入命令

```bash
/ fsck failed
```

可快速定位出现问题的 log ，红字显示的就是问题所在。

```bash
failed to xxxx /dev/sdb5
```

问题最终出现在 sdb5 磁盘分区上，很大概率是上一步的操作路径，对该挂载目录进行修复即可。(退出日志查看)

```bash
fsck -y /dev/sdb5
```

然后进行修复，提示 文件会丢失、是否确认修复等等信息，修复完成后重启即可。