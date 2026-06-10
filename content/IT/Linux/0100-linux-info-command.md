---
title: Linux info 命令详解
section: IT
category: Linux
discussion_id: D_kwDOS1Ul_s4AnB0F
discussion_url: 'https://github.com/yuanchaodu/blog/discussions/10'
---

# Linux info 命令详解

<img src="images/Linux.svg" width="300">

`info` 是 GNU（GNU's Not Unix）项目提供的在线帮助系统，可以看作是 `man` 命令的增强版。许多 GNU 软件（如 `gcc`、`bash`、`coreutils`）的官方文档首先以 Info 格式发布，因此有些内容比 `man` 更详细。

简单理解：

* `man`：像一本工具手册，快速查命令用法。
* `info`：像一本技术书籍，内容更完整、更系统。

---

## 一、基本语法

```bash
info [选项] [主题]
```

查看 ls 命令文档：

```bash
info ls
```

查看 bash 文档：

```bash
info bash
```

打开 Info 主目录：

```bash
info
```

---

## 二、Info 文档特点

与 `man` 不同，Info 文档采用树状结构组织内容。

例如：

```text
Coreutils
├── ls
├── cp
├── mv
├── rm
└── chmod
```

可以在不同章节之间跳转，类似浏览网页。

---

## 三、常用操作

进入 Info 页面后：

| 按键          | 功能             |
| ----------- | -------------- |
| `n`         | 下一节点（Next）     |
| `p`         | 上一节点（Previous） |
| `u`         | 返回上级节点（Up）     |
| `l`         | 返回上一浏览位置       |
| `t`         | 返回目录首页         |
| `Space`     | 下一页            |
| `Backspace` | 上一页            |
| `Tab`       | 跳转到下一个链接       |
| `Enter`     | 打开当前链接         |
| `/关键字`      | 搜索             |
| `q`         | 退出             |

---

## 四、常用参数

### 1. 查看某个主题

```bash
info grep
```

查看 grep 文档。

---

### 2. 打开目录首页

```bash
info
```

显示所有已安装的 Info 文档。

---

### 3. 搜索内容

```bash
info --apropos=keyword
```

例如：

```bash
info --apropos=network
```

搜索与 network 相关的 Info 文档。

---

### 4. 查看指定节点

```bash
info coreutils ls
```

直接查看 Coreutils 文档中的 ls 章节。

---

### 5. 输出纯文本

```bash
info --output=ls.txt ls
```

将文档保存到文件。

---

### 6. 显示版本

```bash
info --version
```

---

## 五、Info 文档结构

一个完整的 Info 文档通常包含：

```text
Top
├── Introduction
├── Tutorial
├── Commands
├── Examples
├── Advanced Features
└── Reference
```

例如 Bash：

```bash
info bash
```

主要章节：

```text
Bash Features
├── Shell Syntax
├── Variables
├── Functions
├── Redirections
├── Job Control
├── Builtin Commands
└── Programming
```

这部分内容通常比：

```bash
man bash
```

详细得多。

---

## 六、常见示例

### 查看 GCC 文档

```bash
info gcc
```

查看编译选项：

```bash
info gcc "Option Summary"
```

---

### 查看 Coreutils 文档

```bash
info coreutils
```

这是 GNU 核心工具集文档。

包括：

```text
ls
cp
mv
rm
mkdir
chmod
chown
```

全部命令的详细说明。

---

### 查看 Bash 编程文档

```bash
info bash
```

内容包括：

```text
变量
函数
条件判断
循环
数组
重定向
管道
```

对于 Shell 开发非常有价值。

---

## 七、man 与 info 的区别

| 对比项      | man  | info |
| -------- | ---- | ---- |
| 目标       | 快速查阅 | 深入学习 |
| 内容长度     | 简洁   | 详细   |
| 结构       | 单页文档 | 树状导航 |
| 超链接      | 无    | 有    |
| GNU 项目支持 | 一般   | 最完整  |
| 学习体验     | 查字典  | 看电子书 |

例如查看 `tar`：

```bash
man tar
```

得到：

```text
命令说明
参数列表
示例
```

而：

```bash
info tar
```

会得到：

```text
tar基础
归档原理
压缩格式
增量备份
恢复方法
高级选项
脚本自动化
```

---

## 八、info 文件存放位置

通常位于：

```bash
/usr/share/info/
```

查看：

```bash
ls /usr/share/info
```

可能看到：

```text
bash.info.gz
coreutils.info.gz
gcc.info.gz
grep.info.gz
tar.info.gz
```

---

## 九、安装 Info 文档

有些精简版 Linux 系统未安装 Info。

查看：

```bash
which info
```

安装方法：

### Debian/Ubuntu

```bash
sudo apt install info
```

### RHEL/CentOS

```bash
sudo dnf install texinfo
```

或

```bash
sudo yum install texinfo
```

### openSUSE

```bash
sudo zypper install texinfo
```

---

## 十、实际工作中的建议

对于运维人员和开发人员，可以按以下顺序查资料：

### 快速查看

```bash
ls --help
```

### 查看完整参数

```bash
man ls
```

### 深入学习原理和高级功能

```bash
info ls
```

或者：

```bash
info coreutils
```

---

## 常用组合总结

```bash
# 查看帮助
info grep

# 查看 Bash 全文档
info bash

# 查看 GCC 文档
info gcc

# 查看 GNU 核心工具文档
info coreutils

# 搜索主题
info --apropos=network

# 返回首页
info

# 导出文档
info --output=doc.txt grep
```

对于 Linux 运维和脚本开发来说，可以记住一个简单原则：

> **`--help` 解决“怎么用”，`man` 解决“参数是什么”，`info` 解决“为什么这样设计以及还能做什么”。**

因此，当你学习 `bash`、`gcc`、`make`、`tar`、`coreutils` 等 GNU 工具时，`info` 往往比 `man` 更值得深入阅读。
