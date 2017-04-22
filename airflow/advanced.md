# Advanced Configuration

## 配置``celery``集群

``airflow``可以很方便的使用``celery``进行平行扩展，步骤如下：

* 按照 [Installation](installation.md) 和 [Configuration](configuration.md) 章节设置好主节点；

* 讲``$AIRFLOW_HOME``目录完整拷贝至``celery``其它工作节点上;

* 确保在``airflow.cfg``中，例如``broker_url``以及``celery_result_backend``等地址都指向同一个位置。

* 在其它所有工作节点上运行``airflow initdb``；

* 最后在工作节点上运行``airflow worker``。

## 在``worker``间传输代码

``airflow``默认情况下，使用``pickle``模块传输``dag``中的代码。这种情况下，有的时候不是很稳定，因为有很多用户自定义对象，也许并无法被``pickle``模块序列化。

如果我们可以保证所有的工作节点的Python环境都是一致的话，我们可以直接传输dag的python代码的文本形式。要做到这一点，可以在``airflow.cfg``文件中修改如下行：

```
donot_pickle = True
```

## 不显示样例dags