## Q

使用 centernet 训练数据可能会出现显卡崩溃的情况，此时可能是显卡驱动出现了问题，可以通过多种方法重新安装驱动。

## S

### Software & Updates

打开 Ubuntu Software & updates 软件，选择 Additional Drivers ，安装推荐的驱动，在网络好的环境下安装成功率较高。

![[additions/additional-driver.png]]

### Download suitable editions

查看显卡型号，在nvidia官网查看对应显卡的驱动，下载的文件格式为 NVIDIA_Linux_x86_64_xxx_.run ，安装显卡驱动前需要卸载当前的驱动，也要禁用ubuntu的开源驱动 nouveau ，末尾添加 `blacklist nouveau` 。

```bash
sudo apt --purge nvidia*
sudo vi /etc/modmodprobe.d/blacklist-nvidia-nouveau.conf
```

这样就可以开始重新安装显卡驱动，网上说需要执行 `sudo systemctl lightdm stop`，但是本机不存在该文件，直接执行也成功了。

```bash
sudo chmod NVIDIA_xxx.run
sudo ./NVIDIA_XXX.run
```

安装完成后重启测试是否安装成功

```bash
nvidia-smi
```
