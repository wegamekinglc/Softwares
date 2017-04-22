# Installation

## 运行环境

只支持``Linux``，推荐使用``ubuntu 16.04``。``python``版本只测试过``python3``。

## 准备

下面的依赖，需要在安装airflow之前完成：

```
pymymsql
mysqlclient
celery
flower
rabbitmq
mysql-server
mysql-client
libmysqlclient-dev
```

其中：

* ``celery``：分布式的任务队列；
* ``flower``：``celery``的监控系统；
* ``rabbitmq``：``celery``依赖的组件之一

## 安装

绝大多数的模块都可以通过``Linux``下的标准安装模式``apt``以及``python``安装工具``pip``完成安装。

```
pip install -U airflow
```

安装完成之后，可以进入``airflow``安装目录下的``example_dags``，删除所有文件。这样在配置好``airflow``之后不会有多余的测试用的任务。
