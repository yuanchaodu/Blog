---
title: Linux rm 命令
section: IT
category: Linux
discussion_id: D_kwDOS1Ul_s4AnDRo
discussion_url: 'https://github.com/yuanchaodu/blog/discussions/30'
---

# Linux rm 命令

<img src="images/Linux.svg" width="300">

`rm`（remove）是 Linux 中用于**删除文件和目录**的命令。它直接从文件系统中删除数据，通常不会进入回收站，因此使用时要特别谨慎。

## 基本语法

```bash
rm [选项] 文件或目录
```

## 常用用法

### 1. 删除单个文件

```bash
rm test.txt
```

删除当前目录下的 `test.txt` 文件。

---

### 2. 删除多个文件

```bash
rm file1.txt file2.txt file3.txt
```

一次删除多个文件。

---

### 3. 删除目录

删除目录需要使用 `-r`（recursive，递归）参数：

```bash
rm -r mydir
```

删除 `mydir` 目录及其所有内容。

---

### 4. 强制删除

```bash
rm -f test.txt
```

参数说明：

* `-f`：force，强制删除
* 不提示确认
* 文件不存在时也不报错

---

### 5. 递归强制删除目录

```bash
rm -rf mydir
```

这是 Linux 中最常见、也最危险的命令之一。

参数说明：

* `-r`：递归删除
* `-f`：强制删除

删除目录及其所有子目录和文件。

---

### 6. 删除时询问确认

```bash
rm -i test.txt
```

删除前会提示：

```text
rm: remove regular file 'test.txt'?
```

输入：

```text
y
```

确认删除。

---

### 7. 删除多个文件时逐个确认

```bash
rm -ri mydir
```

递归删除，并对每个文件进行确认。

---

## 常用选项

| 选项      | 说明       |
| ------- | -------- |
| -f      | 强制删除，不提示 |
| -i      | 删除前询问    |
| -r 或 -R | 递归删除目录   |
| -v      | 显示删除过程   |
| --help  | 查看帮助     |

例如：

```bash
rm -rv mydir
```

输出：

```text
removed 'mydir/file1'
removed 'mydir/file2'
removed directory 'mydir'
```

---

## 通配符使用

### 删除所有 txt 文件

```bash
rm *.txt
```

---

### 删除以 log 开头的文件

```bash
rm log*
```

例如删除：

```text
log1.txt
log2.txt
log20250611.log
```

---

### 删除当前目录所有文件

```bash
rm *
```

注意：

* 不会删除子目录
* 如果存在目录会报错

---

### 删除当前目录所有内容

```bash
rm -rf *
```

会删除当前目录下所有文件和目录。

---

## 危险命令示例

### 删除根目录（现代 Linux 通常会阻止）

```bash
rm -rf /
```

或者：

```bash
rm -rf /*
```

这会导致系统文件被删除，系统无法正常运行。

现代版本的 GNU rm 默认启用了：

```bash
--preserve-root
```

用于保护根目录。

---

## 查看 rm 命令帮助

```bash
man rm
```

或：

```bash
rm --help
```

---

## 企业环境中的安全建议

### 建议 1：默认开启交互确认

在 `~/.bashrc` 中添加：

```bash
alias rm='rm -i'
```

这样执行：

```bash
rm file.txt
```

会先询问确认。

---

### 建议 2：删除前先查看

例如：

```bash
ls *.log
rm *.log
```

先确认匹配的文件，再执行删除。

---

### 建议 3：重要目录使用 find 预览

先查看：

```bash
find /data/logs -name "*.log"
```

确认无误后：

```bash
find /data/logs -name "*.log" -delete
```

---

## rm 与 rmdir 的区别

| 命令    | 删除文件 | 删除非空目录  | 删除空目录 |
| ----- | ---- | ------- | ----- |
| rm    | ✓    | ✓（需 -r） | ✓     |
| rmdir | ✗    | ✗       | ✓     |

例如：

```bash
rmdir emptydir
```

只能删除空目录。

---

简单记忆：

* `rm file.txt`：删除文件
* `rm -r dir`：删除目录
* `rm -f file.txt`：强制删除文件
* `rm -rf dir`：强制递归删除目录（最常用，也最危险）
