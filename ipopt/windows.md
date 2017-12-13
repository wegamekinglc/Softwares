# Installation on Windows

## Using cygwin

* 下载：[cygwin](http://www.cygwin.com/)

* 安装必要的依赖：``patch``，``wget``，``curl``等
 
* 重命名 ``$INSTALL_DIR/usr/bin/link.exe`` 为 ``$INSTALL_DIR/usr/bin/link.bak``, 避免和MSVC 的link.exe抵触。

## Install VS2015 and Intel fortran compiler

* VS2015 for c/c++ compiler cl

* Intel fortran compiler ifort

## Set up envirement

* 编辑 ``Cygwin.bat``，增加：

```bash
call "D:\Program Files (x86)\Microsoft Visual Studio 14.0\VC\bin\amd64\vcvars64.bat"
call "D:\Program Files (x86)\IntelSWTools\compilers_and_libraries_2017.2.187\windows\bin\ifortvars.bat" -arch intel64 vs2015
```

在cmd中确保可以找到cl和ifort。

## Update old scripts

* config.guess

 ```bash
 curl -o config.guess 'http://git.savannah.gnu.org/gitweb/?p=config.git;a=blob_plain;f=config.guess;hb=HEAD'
 ```

* config.sub

 ```
  curl -o config.sub 'http://git.savannah.gnu.org/gitweb/?p=config.git;a=blob_plain;f=config.sub;hb=HEAD'
 ```

需要同时更新Ipopt以及ThirdParty目录下所有的同名文件。

## Modification

在 ``Ipopt\src\Common\config_default.h`` 加入下面的一行：

```cpp
#define HAVE_SNPRINTF 1
```

## Build

```bash
./configure --prefix=/cygdrive/d/dev/svn/CoinIpopt2 --disable-shared --with-mumps=no --with-asl=no CC=cl CXX=cl F77=ifort FC=ifort CXXFLAGS="-MD -Ox -nologo -D_CRT_SECURE_NO_DEPRECATE -DNDEBUG" CFLAGS="-MD -Ox -nologo -D_CRT_SECURE_NO_DEPRECATE -DNDEBUG" FFLAGS="-MD -Ox -fpp -nologo"
make
make install
```
