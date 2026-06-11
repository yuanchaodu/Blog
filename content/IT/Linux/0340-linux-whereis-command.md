---
title: Linux whereis 命令
section: IT
category: Linux
discussion_id: D_kwDOS1Ul_s4AnDZK
discussion_url: 'https://github.com/yuanchaodu/blog/discussions/34'
---

# Linux whereis 命令

<img src="images/Linux.svg" width="300">

`whereis` 是 Linux 中用于**查找命令、源代码文件和帮助文档位置**的工具。它比 `which` 查找范围更广，但不像 `find` 那样遍历整个文件系统，因此速度很快。

## 一、基本语法

```bash
whereis [选项] 文件名
```

例如：

```bash
whereis ls
```

输出：

```bash
ls: /usr/bin/ls /usr/share/man/man1/ls.1.gz
```

表示：

* `/usr/bin/ls`：可执行程序
* `/usr/share/man/man1/ls.1.gz`：帮助文档

---

## 二、常见用法

### 1. 查找命令的位置

```bash
whereis python
```

示例输出：

```bash
python: /usr/bin/python3.12 /usr/lib/python3.12 /usr/share/man/man1/python.1.gz
```

---

### 2. 只查找二进制文件

使用 `-b` 参数：

```bash
whereis -b python
```

输出：

```bash
python: /usr/bin/python3.12
```

---

### 3. 只查找帮助文档

使用 `-m` 参数：

```bash
whereis -m python
```

输出：

```bash
python: /usr/share/man/man1/python.1.gz
```

---

### 4. 只查找源代码

使用 `-s` 参数：

```bash
whereis -s bash
```

如果系统安装了源码，可能输出：

```bash
bash: /usr/src/bash
```

---

### 5. 查找多个命令

```bash
whereis ls cp mv
```

输出：

```bash
ls: /usr/bin/ls /usr/share/man/man1/ls.1.gz
cp: /usr/bin/cp /usr/share/man/man1/cp.1.gz
mv: /usr/bin/mv /usr/share/man/man1/mv.1.gz
```

---

## 三、与 which 的区别

| 命令        | 功能                     |
| --------- | ---------------------- |
| `which`   | 查找当前环境变量 PATH 中实际执行的命令 |
| `whereis` | 查找命令、源码、帮助文档           |
| `find`    | 在指定目录递归搜索文件            |
| `locate`  | 通过数据库快速查找文件            |

例如：

```bash
which python
```

输出：

```bash
/usr/bin/python
```

而：

```bash
whereis python
```

输出：

```bash
python: /usr/bin/python /usr/share/man/man1/python.1.gz
```

可以看到 `whereis` 返回的信息更丰富。

---

## 四、常用选项

| 选项   | 说明            |
| ---- | ------------- |
| `-b` | 只查找二进制程序      |
| `-m` | 只查找 man 帮助文档  |
| `-s` | 只查找源代码        |
| `-u` | 查找不符合条件的文件    |
| `-B` | 指定查找二进制文件目录   |
| `-M` | 指定查找 man 文档目录 |
| `-S` | 指定查找源码目录      |

---

## 五、实用示例

### 查看 nginx 安装位置

```bash
whereis nginx
```

输出类似：

```bash
nginx: /usr/sbin/nginx /usr/share/nginx
```

---

### 查看 mysql 位置

```bash
whereis mysql
```

输出类似：

```bash
mysql: /usr/bin/mysql /usr/share/man/man1/mysql.1.gz
```

---

### 查找没有帮助文档的程序

```bash
whereis -u -m *
```

这会列出缺少 man 手册的程序。

---

## 六、工作原理

`whereis` 不会像 `find` 一样遍历整个磁盘，而是搜索预定义目录，例如：

```text
/bin
/usr/bin
/usr/sbin
/usr/local/bin
/usr/share/man
/usr/src
```

因此：

* 查询速度快
* 结果有限
* 可能找不到安装在特殊目录中的文件

---

## 典型运维场景

查看某个命令实际安装在哪：

```bash
whereis docker
whereis java
whereis python
whereis nginx
```

排查命令版本冲突时，可结合：

```bash
which python
whereis python
type python
```

三者一起使用，能够快速判断系统中是否安装了多个版本以及当前实际执行的是哪个版本。
