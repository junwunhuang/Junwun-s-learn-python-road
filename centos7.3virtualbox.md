### 1、centos7.3系统备份

首先，用管理员身份进入根目录：

```linux
su root
cd /
```

接着，备份系统：

```linux
tar cvpzf backup.tgz --exclude=/proc --exclude=/lost+found --exclude=/mnt --exclude=/sys --exclude=backup.tgz /
```

让我们来简单看一下这个命令：

“tar”当然就是我们备份系统所使用的程序了。

“cvpfz”是tar的选项，意思是“创建档案文件”、“保持权限”\(保留所有东西原来的权限\)、“使用gzip来减小文件尺寸”。

“backup.gz”是我们将要得到的档案文件的文件名。

“/”是我们要备份的目录，在这里是整个文件系统。

在 档案文件名“backup.gz”和要备份的目录名“/”之间给出了备份时必须排除在外的目录。有些目录是无用的，例如“/proc”、“/lost+ found”、“/sys”。当然，“backup.gz”这个档案文件本身必须排除在外，否则你可能会得到一些超出常理的结果。如果不把“/mnt”排 除在外，那么挂载在“/mnt”上的其它分区也会被备份。另外需要确认一下“/media”上没有挂载任何东西\(例如光盘、移动硬盘\)，如果有挂载东西， 必须把“/media”也排除在外。

### 2、安装virtualB0x

```linux
# cd /etc/yum.repos.d/
# wget http://download.virtualbox.org/virtualbox/rpm/rhel/virtualbox.repo
# yum install VirtualBox-5.1
```



