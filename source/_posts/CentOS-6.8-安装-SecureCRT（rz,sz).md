---
title: CentOS 6.8 安装 SecureCRT（rz,sz)
date: 2017年5月24日 10:24:39
tags:
- CentOS
- Linux
categories:
- 笔记
---

#### 1.安装 lrzsz

```shell
yum install lrzsz
```

#### 2.rz sz 使用

- rz中的r意为received（接收），输入rz时、意为服务器接收文件，既将文件从本地上传到服务器。
- sz中的s意为send（发送），输入sz时、意为服务器要发送文件，既从服务器发送文件到本地，或是说本地从服务器上下载文件。

> 注：不论是send还是received，动作都是在服务器上发起的。

##### 2.1 rz

输入rz,回车后在弹出的选择框里面选择文件，可以指定多个文件。**选中的文件将被上传到rz命令的目录中**

##### 2.2 sz

- 下载一个文件 ：`sz filename`
- 下载多个文件 ：`sz filename1 filename2`
- 下载dir目录下的所有文件，不包含dir下的文件夹 ：`sz dir/*`

