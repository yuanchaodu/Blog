---
title: Linux Shell 类型介绍
section: IT
category: Linux
---

# Linux Shell 类型介绍

<img src="images/Linux.svg" width="300">

在 Linux 中，**Shell（命令解释器）** 是用户与操作系统内核之间的桥梁。用户输入命令后，Shell 负责解析命令、调用程序并返回结果。

目前 Linux 常见的 Shell 类型主要有以下几种。

## 1. Bourne Shell（sh）

Bourne Shell 是最早广泛使用的 Unix Shell，由 Stephen Bourne 开发。

特点：

* Shell 的经典实现
* 语法简单
* 可移植性强
* 现代 Linux 中通常只是一个兼容链接

查看系统中的 sh：

```bash
ls -l /bin/sh
```

在不同发行版中：

* Ubuntu/Debian 通常链接到 Dash
* CentOS/RHEL 通常链接到 Bash

适用场景：

* 系统启动脚本
* 需要兼容各种 Unix 系统的脚本

---

## 2. Bash（Bourne Again Shell）

Bash 是目前 Linux 最常用的 Shell。

开发组织：

GNU Project

特点：

* 兼容 sh
* 命令历史记录
* 自动补全
* 命令别名
* 数组支持
* 条件判断增强

查看当前 Shell：

```bash
echo $SHELL
```

查看 Bash 版本：

```bash
bash --version
```

优点：

* 学习资料丰富
* 几乎所有 Linux 发行版默认支持
* 运维人员最常使用

适用场景：

* Linux 运维
* Shell 脚本开发
* 自动化任务

---

## 3. C Shell（csh）

C Shell 的语法参考了 C 语言。

特点：

* 类似 C 语言风格
* 支持历史命令功能
* 支持别名

示例：

```csh
if ($a > 10) then
    echo "OK"
endif
```

缺点：

* 脚本能力较弱
* 可移植性较差

目前已较少使用。

---

## 4. Tcsh

Tcsh 是 C Shell 的增强版。

特点：

* 命令补全
* 命令编辑
* 历史记录增强
* 交互体验优于 csh

应用场景：

* 老式 Unix 系统
* 部分科研机构环境

---

## 5. Korn Shell（ksh）

Korn Shell 由 David Korn 开发。

特点：

* 兼容 sh
* 性能优秀
* 编程能力强
* 支持函数

曾经在企业 Unix 系统中非常流行：

* AIX
* HP-UX
* Solaris

示例：

```ksh
function hello {
    print "Hello"
}
```

适用场景：

* 企业级 Unix 环境
* 大型自动化脚本

---

## 6. Z Shell（zsh）

Zsh 是近年来最受欢迎的 Shell 之一。

特点：

* 功能非常丰富
* 智能补全
* 拼写纠错
* 插件机制
* 主题支持

配合：

* [Oh My Zsh](https://ohmyz.sh?utm_source)

后可获得非常优秀的终端体验。

例如：

```bash
git che<Tab>
```

自动补全：

```bash
git checkout
```

适用场景：

* 开发人员
* DevOps 工程师
* 日常 Linux 使用

目前 macOS 已默认采用 Zsh。

---

## 7. Dash（Debian Almquist Shell）

Dash 是一个轻量级 Shell。

特点：

* 启动速度快
* 占用资源少
* 严格遵循 POSIX 标准

Ubuntu 中：

```bash
/bin/sh -> /bin/dash
```

适用场景：

* 系统启动脚本
* Docker 镜像
* 嵌入式 Linux

优点：

* 执行速度比 Bash 快

缺点：

* 不支持 Bash 的许多扩展功能

---

## 8. Fish（Friendly Interactive Shell）

Fish 是现代化程度很高的 Shell。

特点：

* 开箱即用
* 自动建议
* 彩色语法高亮
* 配置简单

示例：

```fish
git che
```

直接提示：

```fish
git checkout
```

无需额外插件。

官方网站：

[Fish Shell](https://fishshell.com?utm_source)

适用场景：

* Linux 桌面用户
* 开发人员
* Shell 初学者

---

# 各类 Shell 对比

| Shell | 默认兼容 sh | 自动补全  | 脚本能力  | 启动速度  | 当前流行度 |
| ----- | ------- | ----- | ----- | ----- | ----- |
| sh    | ★★★★★   | 无     | ★★★   | ★★★★★ | ★★    |
| bash  | ★★★★★   | ★★★   | ★★★★★ | ★★★   | ★★★★★ |
| csh   | ★       | ★★    | ★★    | ★★★   | ★     |
| tcsh  | ★       | ★★★   | ★★    | ★★★   | ★     |
| ksh   | ★★★★★   | ★★★   | ★★★★  | ★★★★  | ★★    |
| zsh   | ★★★★★   | ★★★★★ | ★★★★★ | ★★★   | ★★★★★ |
| dash  | ★★★★★   | ★     | ★★    | ★★★★★ | ★★★   |
| fish  | ★★      | ★★★★★ | ★★★   | ★★★   | ★★★★  |

---

# 如何查看系统支持哪些 Shell

查看已安装的 Shell：

```bash
cat /etc/shells
```

示例输出：

```text
/bin/sh
/bin/bash
/bin/dash
/bin/zsh
/usr/bin/fish
```

查看当前用户使用的 Shell：

```bash
echo $SHELL
```

查看当前正在运行的 Shell：

```bash
echo $0
```

---

# 选择建议

对于企业信息化、服务器运维和自动化脚本开发场景，可以这样选择：

| 场景          | 推荐 Shell    |
| ----------- | ----------- |
| Linux 运维    | Bash        |
| 自动化脚本       | Bash / Dash |
| 跨平台 Unix 脚本 | sh / Dash   |
| 开发人员日常使用    | Zsh         |
| 桌面用户        | Zsh / Fish  |
| 嵌入式系统       | Dash        |
| 老旧 Unix 系统  | Ksh         |

如果您主要从事企业 IT 运维、Linux 服务器管理和自动化脚本编写，建议重点掌握 **Bash → Zsh → Dash** 这三种：

* Bash：事实上的 Linux 标准
* Zsh：提升个人工作效率
* Dash：理解系统启动脚本和容器环境

掌握这三种 Shell 后，基本可以覆盖 90% 以上的 Linux 实际应用场景。