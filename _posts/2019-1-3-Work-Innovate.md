---
layout:    post
title:     软件相关知识
date:      2019-1-4 22:18:18
summary:  专业知识
categories: ditie 
tags: ISCS
excerpt: 记录综合监控的技巧和攻关项目。
mathjax: true
---
###### 获取电脑CPU 和内存

有时候我们使用Windows图形界面查看CPU和内存使用率并不方便，比如说访问远程电脑时，这时候我们可以使用Windows自带的PowerShell 查看：

Windows10使用命令行查看CPU使用率和RAM使用率
查看CPU:

```
	Get-WmiObject win32_processor | Measure-Object -property LoadPercentage -Average | Select Averagechch
```
Windows10使用命令行查看CPU使用率和RAM使用率
查看内存使用率：

```
    Get-WmiObject win32_OperatingSystem |%{"Total Physical Memory: {0}KB`nFree Physical Memory : {1}KB`nTotal Virtual Memory : {2}KB`nFree Virtual Memory : {3}KB" -f $_.totalvisiblememorysize, $_.freephysicalmemory, $_.totalvirtualmemorysize, $_.freevirtualmemory}
```

Windows10使用命令行查看CPU使用率和RAM使用率
可以使用PowerShell远程登陆其他主机，并运行以上程序，即可以查看远方主机使用情况。

在这里也说下远程登陆的方法：

本机用管理员权限启动 PowerShell，执行下面的命令：
 Enable-PSRemoting –Force
2.远程主机运行:

Enable-PSRemoting -Force
Set-Item -Path WSMan:localhostclient	rustedhosts -Value * -Force
Disable-PSRemoting -forcezh
这一步设置信任主机为“*”，Powershell将允许你与任何IP或机器名联系，公网慎用。不用时你可以运行以下命令关闭：

Disable-PSRemoting 
3.连接远程主机：

Enter-PSSession 192.168.3.1 -Credential abc（密码）administrator（账户）

