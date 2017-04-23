# Installation

本篇介绍如何在`Ubuntu 16.04`上安装`CUDA`工具包，包括`cudnn`的部分。

## 下载

首先在官网下载页面：[CUDA Download](https://developer.nvidia.com/cuda-downloads) 找到对应的最新安装文件：

```
cuda-repo-ubuntu1604_8.0.61-1_amd64.deb
```

以及`cudnn`安装包：

```
libcudnn6-dev_6.0.20-1+cuda8.0_amd64.deb
```

## 安装

安装官网指示，如果下载的是网络安装板`deb`文件，安装`CUDA`运行如下脚本：

```
$ sudo dpkg -i cuda-repo-ubuntu1604_8.0.61-1_amd64.deb
$ sudo apt-get update
$ sudo apt-get install cuda
```

在安装完成后，添加下面的行进入`～/.bashrc`文件：

```

```

安装`cudnn`的