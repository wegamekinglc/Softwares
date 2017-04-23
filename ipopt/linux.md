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
    
`HSL`比较特殊，需要手动下载，[HSL下载页](www.hsl.rl.ac.uk/ipopt/)。下载完成后，将下载包解压，放入`ThirdParty/HSL`目录下。

* 配置安装

在根目录下，运行下面的命令行指令，即可完成编译安装：

```
$ ./configure
$ make
$ make install
```

默认情况下，生产的库文件在根目录下的`lib`文件夹下。


## 使用`openblas`作为链接

* 下载并安装`openblas`

`openblas`可以在[`openblas`](https://github.com/xianyi/OpenBLAS)找到，运行下面的指令即可完成安装：

```
$ make
$ make install PREFIX=/your/path/to/installation
```

`/your/path/to/installation`是你想要安装的目录。最后不要忘了将`openblas`的安装目录加入`LD_LIBRARY_PATH`中。

* 配置`ipopt`的安装

使用如下的命令即可完成：

```
$ ./configure --with-blas="-lopenblas" --with-lapack="-lopenblas"
$ make
$ make install
```

## 使用`mkl`作为链接

在安装完成`Intel(R) Parallel Studio`之后，根据 [Intel Link Advisor](https://software.intel.com/en-us/articles/intel-mkl-link-line-advisor/) 的提示，使用如下的命令即可完成安装：

```
$ ./configure --with-blas="-L${MKLROOT}/lib/intel64 -Wl,--no-as-needed -lmkl_intel_lp64 -lmkl_intel_thread -lmkl_core -liomp5 -lpthread -lm -ldl" --with-lapack="-L${MKLROOT}/lib/intel64 -Wl,--no-as-needed -lmkl_intel_lp64 -lmkl_intel_thread -lmkl_core -liomp5 -lpthread -lm -ldl" CFLAGS="-m64 -I${MKLROOT}/include" CXXFLAGS="-m64 -I${MKLROOT}/include"
$ make
$ make install
```