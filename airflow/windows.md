# Call Windows Programs Remotely

``airflow``只支持在``Linux``上运行。但是很多时候，我们需要的程序只能运行在``Windows``平台上。本章介绍如何在``Linux``上远程运行``Windows``程序。

## ``Linux``

需要安装``openssh``客户端以及服务器：

```
$ sudo apt-get install openssh-server
```

## ``Windows``

需要安装``openssh``的``Windows``服务器，下载地址：

```
https://www.mls-software.com/opensshd.html
```

## 尝试连接

我们可以在``Linux``机器上面尝试连接``Windows``：

```
$ ssh username@hostaddress
```

这时候会显示输入密码，完成输入密码之后，可以登录进入``Windows``电脑。

## 无密码登录

上面的方法每次都需要输入``Windows``用户名对应的密码。实际上，我们可以通过ssh密钥的方式免密码登录。

1. 首先在``Linux``电脑上产生私钥与公钥：

```
$ ssh-keygen -t rsa
```

默认产生地址在：```~/.ssh```目录下。会有两个文件：``id_rsa``以及``id_rsa.pub``，分别是私钥以及公钥。

2. 配置``windows``端

在当前用户目录下新建``.ssh``目录，如下：

```
C:\Users\username\.ssh
```

新建``authorized_keys``文件，并将``id_rsa.pub``文件中的内容追加至``authorized_keys``文件中。

3. 尝试登录

再次从``Linux``机器上尝试连接``Windows``：

```
$ ssh username@hostaddress
```

这个时候应该就不会再需要密码输入了。

## 一些注意事项

* 如果需要在远程运行``Windows``的bat文件，请在bat文件的开头加上下面的语句：

    ```
    chcp 65001
    ```

    将字符编码改为``utf-8``。