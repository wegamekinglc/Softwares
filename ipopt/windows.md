# Installation on Windows

## Using MSYS2

## Install VS2015 and Intel fortran compiler

## Set up envirement

更改msys2_shell.cmd文件，增加以下两行：

```bash
call "D:\Program Files (x86)\Microsoft Visual Studio 14.0\VC\bin\amd64\vcvars64.bat"
call "D:\Program Files (x86)\IntelSWTools\compilers_and_libraries_2017.2.187\windows\bin\ifortvars.bat" -arch intel64 vs2015
```

建议在Windows 10环境下的powershell中运行msys2_shell.cmd，以防止环境变量字符长度过长的问题。

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

在Ipopt\src\Common\config.h加入下面的一行：

```cpp
#define HAVE_SNPRINTF 1
```

## Build

```bash
./configure --prefix=. --disable-shared --with-mumps=no --with-asl=no CC=cl CXX=cl F77=ifort FC=ifort
```