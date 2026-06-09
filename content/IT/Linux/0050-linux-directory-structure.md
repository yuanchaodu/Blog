---
title: Linux 目录结构
section: IT
category: Linux
discussion_id: D_kwDOS1Ul_s4AnA8g
discussion_url: 'https://github.com/yuanchaodu/blog/discussions/5'
---

# Linux 目录结构

<img src="images/Linux.svg" width="300">

Linux 采用树状目录结构，所有文件和目录都从根目录 `/` 开始。无论是硬盘、U盘还是网络存储，都会被挂载到这棵目录树中的某个位置。

## Linux 目录结构示意

```text
/
├── bin
├── boot
├── dev
├── etc
├── home
├── lib
├── media
├── mnt
├── opt
├── proc
├── root
├── run
├── sbin
├── srv
├── sys
├── tmp
├── usr
└── var
```

## 主要目录说明

### `/` 根目录

Linux 文件系统的起点，所有目录和文件都位于其下。

可以把它理解为一棵大树的树根。

---

### `/bin`

存放系统基本命令。

常见命令：

```bash
ls
cp
mv
cat
rm
```

这些命令在单用户模式下也能使用。

---

### `/sbin`

存放系统管理命令。

例如：

```bash
fdisk
reboot
shutdown
mount
```

通常需要管理员权限执行。

---

### `/boot`

系统启动相关文件。

包含：

* Linux内核（vmlinuz）
* 引导程序（GRUB）
* 启动配置文件

例如：

```text
/boot/grub2/
/boot/vmlinuz
```

---

### `/dev`

设备文件目录。

Linux 中一切皆文件，硬盘、U盘、终端等设备都以文件形式存在。

例如：

```text
/dev/sda      第一块硬盘
/dev/sda1     第一块硬盘第1分区
/dev/tty      终端
/dev/null     空设备
```

常见用途：

```bash
echo hello > /dev/null
```

---

### `/etc`

系统配置文件目录。

非常重要。

例如：

```text
/etc/passwd
/etc/shadow
/etc/hosts
/etc/fstab
```

查看主机名配置：

```bash
cat /etc/hostname
```

---

### `/home`

普通用户的家目录。

例如：

```text
/home/nick
/home/tom
/home/jerry
```

用户登录后默认进入自己的 Home 目录。

查看当前目录：

```bash
pwd
```

---

### `/root`

超级用户（root）的家目录。

注意：

```text
/root
```

与

```text
/
```

完全不是同一个目录。

---

### `/lib` 和 `/lib64`

系统共享库文件。

类似于 Windows 的：

```text
C:\Windows\System32\*.dll
```

例如：

```text
/lib/libc.so
```

查看命令依赖库：

```bash
ldd /bin/ls
```

---

### `/usr`

用户应用程序目录。

实际上是系统中最大的目录之一。

包含：

| 目录           | 作用     |
| ------------ | ------ |
| `/usr/bin`   | 普通命令   |
| `/usr/sbin`  | 管理命令   |
| `/usr/lib`   | 程序库    |
| `/usr/share` | 共享资源   |
| `/usr/local` | 本地安装软件 |

例如：

```text
/usr/bin/python3
/usr/local/nginx
```

可以理解为：

> 大部分应用程序安装在 `/usr` 下。

---

### `/var`

可变数据目录。

存放运行过程中不断变化的数据。

例如：

```text
/var/log
/var/spool
/var/cache
/var/tmp
```

日志目录：

```text
/var/log/messages
/var/log/secure
```

查看系统日志：

```bash
tail -f /var/log/messages
```

---

### `/tmp`

临时文件目录。

任何用户都可写入。

系统重启后可能被清空。

例如：

```bash
cd /tmp
```

适合：

* 临时脚本
* 软件安装包
* 测试文件

---

### `/proc`

虚拟文件系统。

不占用磁盘空间，内容来自内核内存。

例如：

```text
/proc/cpuinfo
/proc/meminfo
/proc/version
```

查看CPU信息：

```bash
cat /proc/cpuinfo
```

查看内存：

```bash
cat /proc/meminfo
```

---

### `/sys`

内核设备管理信息。

提供设备和驱动程序状态。

例如：

```text
/sys/class/
/sys/block/
/sys/devices/
```

常用于：

* 设备管理
* 驱动调试
* 性能监控

---

### `/run`

运行时数据目录。

系统启动后创建。

例如：

```text
/run/systemd
/run/lock
/run/user
```

存放：

* PID文件
* Socket文件
* 运行状态信息

---

### `/media`

自动挂载目录。

插入U盘后可能挂载到：

```text
/media/user/Udisk
```

---

### `/mnt`

临时挂载目录。

管理员手动挂载设备时常用。

例如：

```bash
mount /dev/sdb1 /mnt
```

---

### `/opt`

第三方软件安装目录。

例如：

```text
/opt/oracle
/opt/google
```

很多商业软件会安装在这里。

---

### `/srv`

服务数据目录。

例如：

```text
/srv/www
/srv/ftp
```

用于存放服务器提供的数据。

---

## 企业服务器最常关注的目录

作为企业IT运维人员，日常工作中最常接触的是：

| 目录           | 用途     |
| ------------ | ------ |
| `/etc`       | 系统配置   |
| `/var/log`   | 日志分析   |
| `/home`      | 用户数据   |
| `/opt`       | 应用部署   |
| `/usr/local` | 自编译软件  |
| `/tmp`       | 临时文件   |
| `/proc`      | 系统状态查看 |
| `/sys`       | 硬件设备信息 |
| `/boot`      | 启动故障排查 |

---

## 一个形象的理解

可以把 Linux 文件系统看成一座工厂：

| 目录      | 工厂中的角色     |
| ------- | ---------- |
| `/`     | 工厂大门       |
| `/etc`  | 管理制度和配置文件柜 |
| `/home` | 员工办公室      |
| `/root` | 厂长办公室      |
| `/usr`  | 生产车间       |
| `/var`  | 生产记录和日志室   |
| `/tmp`  | 临时堆放区      |
| `/dev`  | 各种设备和机器    |
| `/proc` | 实时监控大屏     |
| `/boot` | 启动控制室      |

这样理解后，记忆 Linux 目录结构会容易很多：**配置看 `/etc`，日志看 `/var/log`，用户数据在 `/home`，程序主要在 `/usr`，设备在 `/dev`，系统状态在 `/proc`。**
