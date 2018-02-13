---
layout: post
title:  "以太坊钱包Ethereum Wallet C盘数据转移"
date:   2018-2-13 21:32:18
categories: Fun
tags: 区块链
excerpt: 以太坊钱包Ethereum Wallet C盘数据转移。
mathjax: true
---

##### 前言

官网自带的Ethereum Wallet（以太坊钱包），默认的同步数据文件目录是 `C:\Users\你的用户名\AppData\Roaming\Ethereum`
由于区块文件占用空间很大（已经超过20G了），而且以后会越来越大，所以导致很多朋友的C盘不够用。我们能不能改变数据路径呢，目前官方的客户端没有可以更改
数据路径的配置。我们只能用其他方法了。

##### 步骤 

1. 将目录`C:\Users\用户名\AppData\Roaming\Ethereum`中的`Ethereum`文件夹**剪切**。放在你`E:\Ethereumdata` 目录下。

2. 使用**管理员身份**运行CMD命令行。一定要用管理员身份，

3. 输入命令：

    mklink /J C:\Users\你的用户名\AppData\Roaming\Ethereum  E:\Ethereumdata

4. 命令成功执行后，会在C:\Users\你的用户名\AppData\Roaming\目录下创建一个Ethereum文件链接。打开后跳转到`E:\Ethereumdata`目录。如图所示：

![创建成功](/Images/2018/sucess.png)

5. 你可以正常启动Ethereum Wallet客户端了，数据已经迁移到`E:\Ethereumdata\Ethereum`中了。

#####注意事项
以上步骤完成后，如出现以下现象，请看第二步是不是以管理员身份运行。
![错误](/Images/2018/error.png)