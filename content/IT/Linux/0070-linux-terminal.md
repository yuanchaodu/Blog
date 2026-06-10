---
title: Linux 终端使用
section: IT
category: Linux
---

# Linux 终端使用

<img src="images/Linux.svg" width="300">

Linux 终端常用内容可以分为几类：

## 1. 进入终端

常见终端软件：

| 环境               | 常见终端                                 |
| ---------------- | ------------------------------------ |
| Ubuntu / GNOME   | GNOME Terminal                       |
| KDE              | Konsole                              |
| macOS 连接 Linux   | Terminal / iTerm2 + SSH              |
| Windows 连接 Linux | Windows Terminal / PuTTY / MobaXterm |
| 服务器远程管理          | SSH                                  |

远程登录常用命令：

```bash
ssh 用户名@服务器IP
```

例如：

```bash
ssh root@192.168.1.10
```

## 2. 文件和目录操作

```bash
pwd          # 查看当前目录
ls           # 查看文件
ls -l        # 详细列表
cd /path     # 进入目录
cd ..        # 返回上一级
mkdir test   # 创建目录
rm file.txt  # 删除文件
rm -r dir    # 删除目录
cp a b       # 复制
mv a b       # 移动或重命名
```

## 3. 查看文件内容

```bash
cat file.txt       # 查看全部内容
less file.txt      # 分页查看
head file.txt      # 查看前几行
tail file.txt      # 查看后几行
tail -f app.log    # 实时查看日志
```

## 4. 系统状态查看

```bash
top          # 查看进程和资源
htop         # 更友好的 top，需安装
df -h        # 查看磁盘空间
du -sh *     # 查看目录大小
free -h      # 查看内存
uptime       # 查看运行时间和负载
```

## 5. 进程管理

```bash
ps aux              # 查看进程
ps aux | grep nginx # 查找进程
kill PID            # 结束进程
kill -9 PID         # 强制结束进程
```

## 6. 网络相关

```bash
ip addr             # 查看 IP 地址
ping 8.8.8.8        # 测试网络连通
curl http://地址     # 请求网页或接口
netstat -tulnp      # 查看端口，部分系统需安装
ss -tulnp           # 查看监听端口
```

## 7. 权限和用户

```bash
chmod +x file.sh    # 增加执行权限
chown user:user file # 修改文件所属用户
sudo 命令            # 以管理员权限执行
whoami              # 查看当前用户
```

## 8. 软件安装

Debian / Ubuntu：

```bash
sudo apt update
sudo apt install 软件名
```

CentOS / RHEL：

```bash
sudo yum install 软件名
```

较新的 RHEL / Rocky / AlmaLinux：

```bash
sudo dnf install 软件名
```

## 9. 服务管理

```bash
systemctl status nginx   # 查看服务状态
systemctl start nginx    # 启动服务
systemctl stop nginx     # 停止服务
systemctl restart nginx  # 重启服务
systemctl enable nginx   # 设置开机自启
```

## 10. 常用快捷键

```text
Ctrl + C    终止当前命令
Ctrl + L    清屏
Ctrl + A    光标到行首
Ctrl + E    光标到行尾
Tab         自动补全
↑ / ↓       查看历史命令
```

日常维护服务器时，最常用的是：

```bash
cd
ls
cat
tail -f
ps aux
grep
df -h
free -h
systemctl
ssh
```

掌握这些命令，基本可以完成 Linux 服务器的日常查看、排障和维护。
