---
title: Linux df 命令
section: IT
category: Linux
---

# Linux df 命令

<img src="images/Linux.svg" width="300">

`df` 是 Linux 中查看**磁盘空间使用情况**的命令。

常用写法：

```bash
df -h
```

含义：以更容易读的方式显示磁盘容量，比如 GB、MB。

示例输出：

```text
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        50G   20G   28G  42% /
tmpfs           2.0G     0  2.0G   0% /dev/shm
```

字段说明：

| 字段         | 含义        |
| ---------- | --------- |
| Filesystem | 文件系统或磁盘分区 |
| Size       | 总容量       |
| Used       | 已使用容量     |
| Avail      | 可用容量      |
| Use%       | 使用百分比     |
| Mounted on | 挂载目录      |

常用参数：

```bash
df -h        # 人类可读格式
df -T        # 显示文件系统类型
df -i        # 查看 inode 使用情况
df -Th       # 同时显示类型和易读容量
df -h /      # 查看根目录所在分区
```

排查磁盘满时，最常用：

```bash
df -h
du -sh /*
```

`df` 看“哪个分区满了”，`du` 看“哪个目录占空间大”。