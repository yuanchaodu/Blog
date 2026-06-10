---
title: Linux pwd 命令
section: IT
category: Linux
discussion_id: D_kwDOS1Ul_s4AnB9r
discussion_url: 'https://github.com/yuanchaodu/blog/discussions/21'
---

# Linux pwd 命令

<img src="images/Linux.svg" width="300">

`pwd` 是 Linux 中最常用的命令之一，全称是 **Print Working Directory（显示当前工作目录）**，用于查看当前终端所在的目录路径。

## 基本语法

```bash
pwd
```

执行后会输出当前所在目录的绝对路径，例如：

```bash
$ pwd
/home/nick/documents
```

表示当前位于 `/home/nick/documents` 目录。

---

## 常见用途

### 1. 查看当前目录

```bash
pwd
```

输出：

```bash
/home/user
```

当你在多个目录之间切换时，可以随时确认自己当前的位置。

---

### 2. 获取真实路径

Linux 中有时会使用软链接（Symbolic Link）。

例如：

```bash
cd /tmp_link
pwd
```

可能输出：

```bash
/tmp_link
```

如果想查看实际对应的物理路径：

```bash
pwd -P
```

输出：

```bash
/var/tmp
```

其中：

* `-P`（Physical）：显示真实物理路径
* `-L`（Logical）：显示逻辑路径（默认）

---

## 常用选项

| 选项       | 说明         |
| -------- | ---------- |
| `pwd`    | 显示当前目录     |
| `pwd -L` | 显示逻辑路径（默认） |
| `pwd -P` | 显示实际物理路径   |

示例：

```bash
pwd -P
```

---

## 与其他命令配合

### 保存当前路径到变量

```bash
CUR_DIR=$(pwd)
echo $CUR_DIR
```

输出：

```bash
/home/user/project
```

---

### 在脚本中获取脚本执行目录

```bash
#!/bin/bash

CURRENT_DIR=$(pwd)
echo "当前目录：$CURRENT_DIR"
```

---

## 实际工作中的应用

例如你进入项目目录：

```bash
cd /opt/app
```

确认位置：

```bash
pwd
```

输出：

```bash
/opt/app
```

然后再执行：

```bash
ls
vim config.ini
```

这样可以避免在错误目录下操作文件。

---

## 与 `cd` 命令的关系

可以把 Linux 文件系统想象成一栋大楼：

* `cd`：进入某个房间
* `pwd`：告诉你当前在哪个房间

例如：

```bash
cd /etc
pwd
```

输出：

```bash
/etc
```

再执行：

```bash
cd /var/log
pwd
```

输出：

```bash
/var/log
```

因此，`pwd` 本质上就是用来查看当前工作目录位置的命令。
