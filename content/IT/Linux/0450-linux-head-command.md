---
title: Linux head 命令
section: IT
category: Linux
---

# Linux head 命令

<img src="images/Linux.svg" width="300">

`head` 是 Linux 中用于**查看文件开头内容**的命令。默认显示文件的前 10 行，常用于查看日志、配置文件或数据文件的开头部分。

## 基本语法

```bash
head [选项] 文件名
```

例如：

```bash
head test.txt
```

输出：

```text
第1行
第2行
...
第10行
```

默认显示前 10 行。

---

## 常用用法

### 1. 查看前 10 行（默认）

```bash
head test.txt
```

等价于：

```bash
head -n 10 test.txt
```

---

### 2. 指定显示前 N 行

显示前 20 行：

```bash
head -n 20 test.txt
```

或者：

```bash
head -20 test.txt
```

输出：

```text
第1行
...
第20行
```

---

### 3. 查看前 N 个字节

显示前 100 个字节：

```bash
head -c 100 test.txt
```

常用于查看二进制文件头部信息。

---

### 4. 查看多个文件

```bash
head file1.txt file2.txt
```

输出类似：

```text
==> file1.txt <==
内容...

==> file2.txt <==
内容...
```

---

### 5. 不显示文件名标题

当查看多个文件时：

```bash
head -q file1.txt file2.txt
```

参数说明：

```text
-q  (quiet)
```

不显示：

```text
==> file1.txt <==
```

这样的文件标题。

---

### 6. 总是显示文件名标题

```bash
head -v file1.txt
```

即使只有一个文件，也显示：

```text
==> file1.txt <==
```

---

## 与管道配合使用

### 查看命令输出的前几行

例如查看进程：

```bash
ps -ef | head
```

查看磁盘信息：

```bash
df -h | head -5
```

查看目录文件：

```bash
ls -l | head
```

---

## 日志分析中的应用

### 查看日志开头

```bash
head /var/log/messages
```

### 查看 CSV 文件前几行

```bash
head sales.csv
```

输出：

```text
id,name,amount
1,Tom,100
2,Jack,200
...
```

用于确认文件格式和字段结构。

---

## head 与 tail 对比

| 命令   | 功能     |
| ---- | ------ |
| head | 查看文件开头 |
| tail | 查看文件末尾 |

例如：

```bash
head logfile.log
```

查看最早的日志。

```bash
tail logfile.log
```

查看最新的日志。

实时监控日志通常使用：

```bash
tail -f logfile.log
```

---

## 实际工作中的常见场景

### 查看配置文件前 30 行

```bash
head -30 nginx.conf
```

### 查看 CSV 数据样本

```bash
head -5 data.csv
```

### 查看系统日志开头

```bash
head /var/log/secure
```

### 查看大文件是否正常生成

```bash
head bigfile.txt
```

无需打开整个文件即可快速确认内容。

---

## 总结

最常用的几个写法：

```bash
head file.txt           # 前10行
head -n 20 file.txt     # 前20行
head -c 100 file.txt    # 前100字节
ps -ef | head           # 查看命令输出前10行
```

在日常 Linux 运维、日志分析和数据处理工作中，`head` 与 `tail`、`grep`、`awk` 经常组合使用，是最基础也最实用的文本查看工具之一。