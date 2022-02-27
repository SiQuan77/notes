# 前言

本文主要会写一些自己在安装和使用podman遇到的一些问题和心得。持续更新..

## 介绍podman

![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/2062381-20211031112439621-211944761.png)

> 下面介绍参考[2. podman -- 简介、安装 - 牛顿撕鸡 - 博客园 (cnblogs.com)](https://www.cnblogs.com/newtonsky/p/15488829.html)和[Podman解析 - 简书 (jianshu.com)](https://www.jianshu.com/p/3fc6eff747ab)。

​	Podman 是一个开源的容器运行时项目，可在大多数 Linux 平台上使用。Podman 提供与 Docker 非常相似的功能。正如前面提到的那样，它不需要在你的系统上运行任何守护进程，并且它也可以在没有 root 权限的情况下运行。 



​	podman（Pod Manager）是 RedHat 推出，在 Linux系统上开发，管理、运行 OCI 的容器。

定位就是 docker 的**替代品**，在使用上与 docker 的体验类似。

- podman 是一个开源 Linux工具，docker 已经是商业化的产品。
- podman 是一个无守护进程的容器引擎，而 docker 是 C/S 架构，服务端需要有一个守护进程

（这意味着无需 systemctl start podman 之类的考虑，可以直接运行 podman，运行程序时，无需考虑服务是否是 active，就是一个程序，可以直接运行）

- podman 普通用户可以运行容器，docker 需要 root 来创建容器
- 可以用于管理任何 OCI 的容器引擎（如 Docker）创建的 Linux容器， 提供了与 Docker 兼容的命令行前端。

# 心得

## 安装

Podman 官网地址：https://podman.io/

Podman 项目地址：https://github.com/containers/libpod



首先通过yum进行安装。

```bash
sudo yum -y install podman
```

当显示以下则说明安装成功

![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/20220227220751.png)

# 遇到的问题
