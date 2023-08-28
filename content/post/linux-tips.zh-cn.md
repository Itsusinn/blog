---
title: "Linux Tips"
description: 
date: 2023-08-27T21:55:07+08:00
image: 
math: 
license: 
hidden: false
comments: true
---

### 创建顶级Btrfs子卷

```bash
$ fdisk -l
$ sudo mount /dev/<part> -o subvolid=5 /mnt
$ cd /mnt
$ sudo btrfs subvolume create <name>
$ sudo btrfs subvolume list /
```

<part>: Btrfs分区名
<name>: 子卷名称

### 挂载Btrfs子卷为交换区

```bash
$ sudo vim /etc/fstab
UUID=<UUID>                        /swap          btrfs   subvol=/<name>,defaults 0 0
/swap/swapfile                     swap           swap    defaults 0 0
$ cd /
$ sudo mkdir swap
$ sudo mount -a
$ sudo btrfs filesystem mkswapfile --size 8g --uuid clear /swap/swapfile
$ sudo swapon /swap/swapfile
$ sudo mount -a
```

<UUID> : Btrfs分区UUID

<name>: 子卷名称