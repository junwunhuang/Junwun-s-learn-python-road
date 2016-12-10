* ### 当我在刚安装好的Centos7（最小模式）下自带的yum源不能使用是，我更换国内yum源所遇到的坑


这时，我首先是想用wget命令下载我准备用的目标网站的yum源配置文件（比如阿里、163网易等，这里我选择的是163网易源）

```
# wget http://xxxxxx
```

可是这时系统报没有wget命令。这就头大了。

网上一般给出的wget安装办法基本是基于yum命令安装的，可这里我不能用yum。。。。。

网上找了半天，我终于发现有人说可以用光盘挂载的办法解决，我想，也可以用U盘挂载。结果我用我安装这个centos7的U盘制作的系统安装盘解决了。

首先，解决U盘挂载问题，插上U盘，输入命令：

```
fdisk -l
```

在出现的内容最后出现了：

![](/assets/1.png)z

在/mnt目录下新建目录作为挂载点：

```
cd /mnt
mkdir usb-fat32
```

挂载我的格式为FAT32的U盘：

```
mount -t vfat /dev/sdb4 /mnt/usb-fat32
```

查看U盘中文件：

```
ls /mnt/usb-fat32
```

卸载U盘：

```
umount /dev/sdb4
```

或

```
umount /mnt/usb-fat32
```



