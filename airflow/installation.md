# Installation

## 运行环境

只支持``Linux``，推荐使用``ubuntu 16.04``。``python``版本只测试过``python3``。

## 准备

下面的依赖，需要在安装airflow之前完成：

```
postgresql
celery
flower
rabbitmq
psycopg2
```

其中：

* ``celery``：分布式的任务队列；
* ``flower``：``celery``的监控系统；
* ``rabbitmq``：``celery``依赖的组件之一；
* ``postgresql``: 在本安装说明中是作为``aiflow``的数据存储以及``celery``的``result_backend``。

## 安装

绝大多数的模块都可以通过``Linux``下的标准安装模式``apt``以及``python``安装工具``pip``完成安装。

``PostgreSQL``可以在官网上下载安装包安装，推荐使用[EnterpriseDB](https://www.enterprisedb.com/downloads/postgres-postgresql-downloads#windows)发行版。

``airflow``主程序的安装方式可以直接使用``pip``：

```
pip install -U apache-airflow
```

安装完成之后，可以进入``airflow``安装目录下的``example_dags``，删除所有文件。这样在配置好``airflow``之后不会有多余的测试用的任务。也可以通过配置``airflow.cfg``配置文件的方式，不显示这些例子，具体请参考：[Advanced](advanced.md)
