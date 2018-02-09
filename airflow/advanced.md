# Advanced Configuration

## 配置``celery``集群

``airflow``可以很方便的使用``celery``进行平行扩展，步骤如下：

* 按照 [Installation](installation.md) 和 [Configuration](configuration.md) 章节设置好主节点；

* 将``$AIRFLOW_HOME``目录完整拷贝至``celery``其它工作节点上;

* 确保在``airflow.cfg``中，
    
    * ``executor=CeleryExecutor``

    * 例如``broker_url``以及``celery_result_backend``等地址都指向同一个位置。

* 在其它所有工作节点上运行``airflow initdb``；

* 最后在工作节点上运行``airflow worker``。

## 配置``dask``集群

``airflow``同样可以很方便的使用``dask``进行扩展，步骤如下：

* 按照 [Installation](installation.md) 和 [Configuration](configuration.md) 章节设置好主节点；

* 将``$AIRFLOW_HOME``目录完整拷贝至``celery``其它工作节点上;

* 按照[dask.distributed](https://distributed.readthedocs.io/en/latest/)文档启动集群；

* 确保在``airflow.cfg``中，
    
    * ``executor=DaskExecutor``

    * ``cluster_address = $CLUSTER_HOST:$CLUSTER_PORT``


### log的集中存储

按照上面的方法配置``worker``的话，已经可以做到平行的scale。但是这时候遇到一个问题，各个``worker``的log都是存在所在机器的本地，``master``节点只能看到自己节点``work``的日志。虽然这并不影响celery集群正常工作，但是在工作出错的时候，部分log的丢失，给debug造成很大的困难。

这个时候需要使用log的集中存储，可以使用类似于云上的方案，我这里使用文件夹的共享。下面的操作在ubuntu 16.04上测试通过：

* 在需要共享的机器上安装：``nfs``

    sudo apt-get install nfs-kernel-server

* 修改``/etc/exports``文件，增加如下的行：

    /your_airflow_home *(rw,sync,no_subtree_check)

* 重启``nfs``

    sudo /etc/init.d/nfs-kernel-server restart
    
* 服务器端开放读写权限
    
    chmod -R 777 /your_airflow_home

* 在另一台主机上挂载该共享目录

    sudo mount -t nfs host:/your_airflow_home /your_airflow_home


## 在``worker``间传输代码

``airflow``默认情况下，使用``pickle``模块传输``dag``中的代码。这种情况下，有的时候不是很稳定，因为有很多用户自定义对象，也许并无法被``pickle``模块序列化。

如果我们可以保证所有的工作节点的Python环境都是一致的话，我们可以直接传输dag的python代码的文本形式。要做到这一点，可以在``airflow.cfg``文件中修改如下行：

```
donot_pickle = True
```

## 不显示样例dags

在``airflow.cfg``文件中将``load_example``的值改为``False``

```
load_examples = False
```
