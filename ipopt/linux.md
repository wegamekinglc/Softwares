# Installation on Linux

本篇中，我们将详细介绍如何在`Ubuntu 16.04`上安装`ipopt`。

## 获取代码

当前最新的代码可以从下面的svn地址获取：

```
$ svn co https://projects.coin-or.org/svn/Ipopt/stable/3.12 CoinIpopt 
```

> 不要从`github`上获取代码，`github`上获取的代码不会带有第三方的依赖。
    
    

## 基础安装

该部分，主要参考自 [Ipopt安装指南](https://www.coin-or.org/Ipopt/documentation/node10.html)：

* 下载第三方组件
    
进入根目录下ThirdParty目录，分别下载如下部件：

    1. ASL
    2. Blas
    3. Lapack
    4. Metis
    5. Mumps
    
`HSL`比较特殊，需要手动下载，[HSL下载页](www.hsl.rl.ac.uk/ipopt/)
