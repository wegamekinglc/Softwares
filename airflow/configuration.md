# Configuration

## 配置``mysql``数据库

### ``airflow``数据库

 ``airflow``需要有一个专用的数据存放任务的信息以及产生的日志。这里使用``mysql``，我们创建如下的数据库：

```
create database airflow;
create user airflow_admin@'%' identified by 'yourpassword';
grant all privileges on airflow.* to airflow_admin@'%';
```

### ``celery``数据库

``celery``可以配置``mysql``作为存储运行结果的数据库。这里我们可以新开一个``database``，或者选择与``airflow``合用。

## 配置``rabbitmq``

``celery``使用``rabbitmq``作为``broker``，默认可以直接使用guest用户和``/``host。这里我们为了方便``airflow``对它的使用，我们对``rabbitmq``进行单独的配置：

```
$ sudo rabbitmqctl add_user airflow yourpassword
$ sudo rabbitmqctl add_vhost airflow_host
$ sudo rabbitmqctl set_user_tags airflow airflow_tag
$ sudo rabbitmqctl set_permissions -p airflow_host airflow ".*" ".*" ".*"
```

## 配置``airflow``

以下配置方法，详细信息可参考：[``airflow``文档](http://airflow.incubator.apache.org/)

### 配置工作目录

``airflow``需要配置自己的工作目录，方法例如：在用户目录下新建``airflow``文件夹，然后

```bash
$ export AIRFLOW_HOME=~/airflow
```

上面这行可以放到用户的``~/.bashrc``文件中，确保下次打开命令行时都会配置这个环境变量。

### 初始化工作目录

运行如下命令：

```bash
$ airflow initdb
```

这个时候``airflow``会初始化一个工作环境，使用``python``自带的``sqlite``作为数据存储。

### 配置``airflow``

在实际的环境中，我们需要使用``mysql``作为工作用数据库，同时需要使用``celery``作为工作引擎。

在``airflow``的工作目录下找到配置文件``airflow.cfg``，做如下的修改：

* 更改工作引擎

```
executor = CeleryExecutor
```

* 设置后台数据库

```
sql_alchemy_conn = mysql+pymysql://airflow_admin:yourpassword@localhost:3306/airflow
```

这里具体的参数请与你设置的``airflow``数据一致。

* 设置``celery``参数

```
broker_url = amqp://airflow:yourpassword@localhost:5672/airflow_host
celery_result_backend = db+mysql://airflow_admin:yourpassword@localhost:3306/airflow
```

## 启动``airflow``

### 初始化

在配置完所有参数以后，需要再次运行以下命令初始化：

```bash
$ airflow initdb
```

### 启动``airflow``的``webserver``

```
$ airflow webserver -p 8080
```

### 启动``shceduler``

```
$ airflow scheduler
```

### 启动``worker``

```
$ airflow worker
```

### 启动``celery``的``flower``监控界面

```
$ airflow flower
```

至此为止整个``airflow``运行环境启动成功！
