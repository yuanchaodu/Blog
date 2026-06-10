---
title: Linux rmdir 命令
section: IT
category: Linux
discussion_id: D_kwDOS1Ul_s4AnCQs
discussion_url: 'https://github.com/yuanchaodu/blog/discussions/27'
---

# Linux rmdir 命令

<img src="images/Linux.svg" width="300">

`rmdir` 是 Linux 中用于**删除空目录**（empty directory）的命令。

## 基本语法

```bash
rmdir [选项] 目录名
```

例如：

```bash
rmdir test
```

如果 `test` 目录为空，则会被删除。

---

## 常用示例

### 1. 删除单个空目录

```bash
rmdir mydir
```

删除当前目录下的 `mydir`。

---

### 2. 同时删除多个空目录

```bash
rmdir dir1 dir2 dir3
```

如果这些目录都是空的，则全部删除。

---

### 3. 递归删除空目录路径

假设目录结构如下：

```text
a/
└── b/
    └── c/
```

且三个目录都为空。

执行：

```bash
rmdir -p a/b/c
```

结果：

```text
a/
b/
c/
```

都会被删除。

参数说明：

```bash
-p
```

表示按照路径逐级删除空目录。

---

### 4. 显示删除过程

```bash
rmdir -pv a/b/c
```

输出类似：

```text
rmdir: removing directory 'a/b/c'
rmdir: removing directory 'a/b'
rmdir: removing directory 'a'
```

其中：

* `-p`：逐级删除
* `-v`：显示详细过程（verbose）

---

## 常用参数

| 参数                           | 说明              |
| ---------------------------- | --------------- |
| `-p`                         | 删除目录及其父目录（如果为空） |
| `-v`                         | 显示详细删除过程        |
| `--ignore-fail-on-non-empty` | 目录非空时忽略错误       |

例如：

```bash
rmdir --ignore-fail-on-non-empty test
```

如果 `test` 非空，不会报错退出。

---

## 与 rm -r 的区别

| 命令       | 删除对象  | 目录必须为空 |
| -------- | ----- | ------ |
| `rmdir`  | 目录    | 是      |
| `rm -r`  | 文件和目录 | 否      |
| `rm -rf` | 文件和目录 | 否，强制删除 |

例如：

目录内容：

```text
test/
└── file.txt
```

执行：

```bash
rmdir test
```

结果：

```text
rmdir: failed to remove 'test': Directory not empty
```

因为目录中还有文件。

而：

```bash
rm -r test
```

会连同目录中的所有文件一起删除。

---

## 查看帮助

```bash
man rmdir
```

或：

```bash
rmdir --help
```

---

## 使用建议

* **删除空目录时优先使用 `rmdir`**，更安全。
* **删除非空目录时使用 `rm -r`**。
* **生产环境中谨慎使用 `rm -rf`**，因为删除后通常无法恢复。

一个常见的运维脚本写法是：

```bash
find /data/logs -type d -empty -exec rmdir {} \;
```

该命令会查找 `/data/logs` 下所有空目录并删除它们。
