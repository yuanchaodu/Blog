---
title: Linux locate 命令
section: IT
category: Linux
---

# Linux locate 命令

<img src="images/Linux.svg" width="300">

`locate` 是 Linux 中用于**快速查找文件和目录**的命令。与 `find` 命令实时遍历文件系统不同，`locate` 查询的是预先建立好的文件索引数据库，因此速度非常快。

## 一、基本语法

```bash
locate [选项] 文件名
```

例如：

```bash
locate nginx.conf
```

输出：

```text
/etc/nginx/nginx.conf
/usr/local/nginx/conf/nginx.conf
```

表示系统中所有名为 `nginx.conf` 的文件。

---

## 二、工作原理

`locate` 不会实时扫描磁盘，而是查询数据库：

```text
/var/lib/mlocate/mlocate.db
```

或（不同发行版可能不同）：

```text
/var/lib/plocate/plocate.db
```

因此：

* 查询速度极快
* 新创建的文件可能查不到
* 删除的文件可能仍然存在于数据库中

---

## 三、更新数据库

### 手动更新

```bash
sudo updatedb
```

执行后重新建立索引。

例如：

```bash
touch /tmp/test.txt

locate test.txt
```

可能查不到。

执行：

```bash
sudo updatedb
```

再查询：

```bash
locate test.txt
```

即可找到。

---

## 四、常用示例

### 1. 查找文件

```bash
locate passwd
```

输出所有包含 `passwd` 的路径。

---

### 2. 精确匹配文件名

```bash
locate -b '\passwd'
```

说明：

* `-b`：只匹配路径最后部分（basename）
* `\` 表示文件名边界

例如：

```bash
locate -b '\nginx.conf'
```

只查找真正叫 `nginx.conf` 的文件。

---

### 3. 忽略大小写

```bash
locate -i readme
```

等同于：

```bash
locate README
locate ReadMe
locate readme
```

一起匹配。

---

### 4. 显示匹配数量

```bash
locate -c log
```

输出：

```text
15234
```

表示找到 15234 条记录。

---

### 5. 限制显示结果数量

```bash
locate -n 10 log
```

仅显示前 10 条结果。

---

### 6. 使用正则表达式

```bash
locate -r '.*\.conf$'
```

查找所有 `.conf` 文件。

例如：

```bash
locate -r '/etc/.*\.conf$'
```

查找 `/etc` 下的配置文件。

---

## 五、与 find 命令比较

| 项目         | locate  | find   |
| ---------- | ------- | ------ |
| 搜索速度       | 极快      | 较慢     |
| 搜索方式       | 查询数据库   | 实时遍历磁盘 |
| 数据实时性      | 依赖数据库更新 | 实时     |
| 支持权限过滤     | 有限      | 强大     |
| 支持时间、大小等条件 | 不支持     | 支持     |
| 适用场景       | 快速定位文件  | 精确查找   |

例如：

### locate

```bash
locate httpd.conf
```

几乎瞬间返回结果。

### find

```bash
find / -name httpd.conf
```

需要遍历目录树，速度较慢。

---

## 六、常见发行版差异

### CentOS / RHEL 7

安装：

```bash
yum install mlocate
```

更新数据库：

```bash
updatedb
```

---

### RHEL 8 / Rocky / AlmaLinux

```bash
dnf install mlocate
```

或：

```bash
dnf install plocate
```

---

### Ubuntu / Debian

现代版本通常使用：

```bash
sudo apt install plocate
```

查看版本：

```bash
locate --version
```

可能显示：

```text
plocate 1.1.x
```

---

## 七、实际运维常用场景

### 查找 Java 安装目录

```bash
locate java | grep bin/java
```

---

### 查找 Oracle 配置文件

```bash
locate listener.ora
```

---

### 查找 SSL 证书

```bash
locate .crt
```

---

### 查找日志目录

```bash
locate logs
```

---

### 查找某个共享库

```bash
locate libssl.so
```

---

## 八、企业环境中的经验

在生产服务器上：

1. **先用 locate 快速定位**

   ```bash
   locate application.yml
   ```

2. **再用 find 精确验证**

   ```bash
   find /opt -name application.yml
   ```

3. 对于大型服务器（数百万文件），`locate` 往往能在毫秒级返回结果，而 `find /` 可能需要数分钟。

因此很多 Linux 运维人员习惯：

```text
已知文件名 → locate
未知文件属性 → find
```

两者配合使用效率最高。