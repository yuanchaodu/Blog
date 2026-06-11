---
title: Linux less 命令
section: IT
category: Linux
discussion_id: D_kwDOS1Ul_s4AnD7M
discussion_url: 'https://github.com/yuanchaodu/blog/discussions/44'
---

# Linux less 命令

<img src="images/Linux.svg" width="300">

`less` 是 Linux 中最常用的分页查看命令之一，用于查看文本文件内容。它比早期的 `more` 功能更强，因此得名“less is more”。

## 一、基本语法

```bash
less 文件名
```

例如：

```bash
less /var/log/messages
```

或：

```bash
less test.txt
```

---

## 二、常见用途

### 1. 查看大文件

```bash
less huge.log
```

与 `cat` 不同，`less` 不会一次性加载全部内容，而是按需读取，因此查看大型日志文件时速度快、内存占用低。

---

### 2. 查看命令输出

```bash
ps -ef | less
```

```bash
journalctl | less
```

```bash
ls -lR | less
```

这样可以分页浏览输出结果。

---

### 3. 查看压缩文件

某些 Linux 发行版支持：

```bash
zless access.log.gz
```

---

## 三、常用操作键

进入 `less` 后，可以使用以下快捷键：

| 按键    | 功能     |
| ----- | ------ |
| ↑ 或 k | 上一行    |
| ↓ 或 j | 下一行    |
| Space | 下一页    |
| b     | 上一页    |
| d     | 下翻半页   |
| u     | 上翻半页   |
| g     | 跳到文件开头 |
| G     | 跳到文件结尾 |
| q     | 退出     |
| h     | 查看帮助   |

---

## 四、搜索功能

### 向下搜索

输入：

```text
/关键字
```

例如：

```text
/error
```

然后回车。

### 搜索下一个匹配项

```text
n
```

### 搜索上一个匹配项

```text
N
```

---

### 向上搜索

```text
?关键字
```

例如：

```text
?warning
```

---

## 五、显示行号

```bash
less -N test.txt
```

效果：

```text
1  first line
2  second line
3  third line
```

---

## 六、实时查看增长中的日志

类似 `tail -f`：

```bash
less +F /var/log/messages
```

或

```bash
less +F app.log
```

此时会持续刷新显示新增内容。

退出实时模式：

```text
Ctrl + C
```

然后继续正常浏览。

---

## 七、忽略大小写搜索

启动时：

```bash
less -i test.txt
```

搜索：

```text
/error
```

会同时匹配：

```text
error
ERROR
Error
```

---

## 八、查看多个文件

```bash
less file1.txt file2.txt file3.txt
```

在 less 中：

```text
:n
```

切换到下一个文件。

```text
:p
```

切换到上一个文件。

---

## 九、常用参数

| 参数 | 作用            |
| -- | ------------- |
| -N | 显示行号          |
| -i | 搜索时忽略大小写      |
| -S | 不自动换行，长行可左右滚动 |
| -F | 文件只有一页时自动退出   |
| -X | 退出后保留屏幕内容     |
| -R | 显示 ANSI 颜色代码  |
| +F | 实时监控文件增长      |

例如：

```bash
less -NR /var/log/messages
```

既显示行号，又保留彩色输出。

---

## 十、运维人员常用组合

### 查看日志并搜索错误

```bash
less /var/log/messages
```

然后：

```text
/error
```

---

### 查看 systemd 日志

```bash
journalctl -xe | less
```

---

### 保留 grep 高亮颜色

```bash
grep --color=always ERROR app.log | less -R
```

其中：

```bash
-R
```

用于让 `less` 正确显示颜色。

---

## 十一、与 cat、more 的区别

| 命令   | 特点          |
| ---- | ----------- |
| cat  | 一次性输出全部内容   |
| more | 只能向下翻页      |
| less | 可上下翻页、搜索、跳转 |

简单理解：

* `cat`：直接把文件倒出来。
* `more`：一页一页往下看。
* `less`：像阅读器一样浏览文件，可搜索、定位、前后翻页。

因此在日常运维、日志分析、系统排错中，`less` 通常是查看文件的首选工具。特别是在查看大型日志文件时，经常会配合：

```bash
grep --color=always "ERROR" app.log | less -R
```

和

```bash
journalctl -xe | less
```

使用。
