# Installation on Windows

## Using MSYS2

* 下载：[msys2](http://www.msys2.org/)

* 安装必要的依赖：
 
 ```
 pacman -S make gcc diffutils pkg-confi tar patch
 ```
 
* 重命名 ``$INSTALL_DIR/usr/bin/link.exe`` 为 ``$INSTALL_DIR/usr/bin/link.bak``, 避免和MSVC 的link.exe抵触。

## Install VS2015 and Intel fortran compiler

* VS2015 for c/c++ compiler cl

* Intel fortran compiler ifort

## Set up envirement

* 编辑 ``$INSTALL_DIR/msys2_shell.cmd`` ，将如下行解除注释

 ```
 rem set MSYS2_PATH_TYPE=inherit
 ```

* 进入 ``msys2_shell.cmd`` 所在目录，运行：

```bash
"D:\Program Files (x86)\Microsoft Visual Studio 14.0\VC\bin\amd64\vcvars64.bat"
"D:\Program Files (x86)\IntelSWTools\compilers_and_libraries_2017.2.187\windows\bin\ifortvars.bat" -arch intel64 vs2015
msys2_shell.cmd
```

建议在Windows 10环境下的powershell中运行msys2_shell.cmd，以防止环境变量字符长度过长的问题。在msys2中确保可以找到cl和ifort。

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
./configure --prefix=. --disable-shared --with-mumps=no --with-asl=no CC=cl CXX=cl F77=ifort FC=ifort
make
make install
```
