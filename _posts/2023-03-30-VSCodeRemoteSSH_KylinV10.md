---
title: VSCode Remote-SSH链接提示administratively prohibited的解决方法
description: 在从RedHat升级到KylinV10时，之前一直可以直接链接的VSCode RemoteSSH无法连接，提示open failed：administratively prohibited，在查阅资料后，确认是新环境的SSH默认配置更严格，因此可以通过配置SSH的方式解决。
categories:
 - linux
tags:
  - solution
  - linux
  - ssh
keywords:
  - vscode
  - remote ssh
  - administratively
  - prohibited
  - ssh
  - kylin
  - linux
  - solution
  - 配置
date: 2023-03-30 00:00:00
updated: 2023-03-30 00:00:00
---

## 概述

在从`RedHat`升级到`KylinV10`时，之前一直可以直接链接的`VSCode RemoteSSH`无法连接，提示`open failed：administratively prohibited`，在查阅资料后，确认是新环境的`SSH`默认配置更严格，因此可以通过配置`SSH`的方式解决。

## 解决方法

我使用了以下方法解决了这个问题。

### 更新OpenSSH

可能是因为系统的`OpenSSH`版本过低，需要更新，这种方法有概率修复问题。

```shell
yum update openssh
```

### 修改ssh默认配置

修改`/etc/ssh/sshd_config`配置项，然后依次找出以下配置项并修改为下面的值：

```text
StrictModes no
AllowTcpForwarding yes
PermitTunnel yes
```

然后重启`ssh`服务，即可正常链接

```shell
systemctl restart sshd
```
