# airflow

## 简介

​    Airflow 是一个使用 python 语言编写的 data pipeline 调度和监控工作流的平台。 Airflow 是通过 DAG（Directed acyclic graph 有向无环图）来管理任务流程的任务调度工具， 不需要知道业务数据的具体内容，设置任务的依赖关系即可实现任务调度。

## 解决问题

- 时间依赖：任务需要等待某一个时间点触发。
- 外部系统依赖：任务依赖外部系统需要调用接口去访问。
- 任务间依赖：任务 A 需要在任务 B 完成后启动，两个任务互相间会产生影响。 
- 资源环境依赖：任务消耗资源非常多， 或者只能在特定的机器上执行。

#### **Airflow**的处理依赖的方式

Airflow 和crontab不同。crontab 可以很好地处理定时执行任务的需求，它是一种依赖管理系统，而且只管理时间上的依赖。Airflow 的核心概念，是 DAG (有向无环图)，DAG 由一个或多个 TASK 组成，而这个 DAG 正是解决了上文所说的任务间依赖。Task A 执行完成后才能执行 Task B，多个Task之间的依赖关系可以很好的用DAG表示完善。

Airflow 完整的支持 crontab 表达式，也支持直接使用 python 的 datatime 表述时间，还可以用 datatime 的 delta 表述时间差。这样可以解决任务的时间依赖问题。

Airflow 可以为任意一个 Task 指定一个抽象的 Pool，每个 Pool 可以指定一个 Slot 数。每当一个 Task 启动时，就占用一个 Slot ，当 Slot 数占满时，其余的任务就处于等待状态。这样就解决了资源依赖问题。

Airflow 中有 Hook 机制，作用时建立一个与外部数据系统之间的连接，比如 Mysql，HDFS，本地文件系统(文件系统也被认为是外部系统)等，通过拓展 Hook 能够接入任意的外部系统的接口进行连接，这样就解决的外部系统依赖问题。

## 安装

参考链接：

https://airflow.apache.org/docs/apache-airflow/stable/start/local.html

1. 创建一个虚拟环境（使用python命令或者anaconda均可，创建一个新环境不容易出现包冲突问题）

2. 使用pip进行安装

   ```
   # airflow needs a home, ~/airflow is the default,
   # but you can lay foundation somewhere else if you prefer
   # (optional)
   export AIRFLOW_HOME=~/airflow
   
   AIRFLOW_VERSION=2.0.1
   PYTHON_VERSION="$(python --version | cut -d " " -f 2 | cut -d "." -f 1-2)"
   # For example: 3.6
   CONSTRAINT_URL="https://raw.githubusercontent.com/apache/airflow/constraints-${AIRFLOW_VERSION}/constraints-${PYTHON_VERSION}.txt"
   # For example: https://raw.githubusercontent.com/apache/airflow/constraints-2.0.2/constraints-3.6.txt
   pip install "apache-airflow==${AIRFLOW_VERSION}" --constraint "${CONSTRAINT_URL}"
   
   # initialize the database
   airflow db init
   
   airflow users create \
       --username admin \
       --firstname Peter \
       --lastname Parker \
       --role Admin \
       --email spiderman@superhero.org
   
   # start the web server, default port is 8080
   airflow webserver --port 8080
   
   # start the scheduler
   # open a new terminal or else run webserver with ``-D`` option to run it as a daemon
   airflow scheduler
   
   # visit localhost:8080 in the browser and use the admin account you just
   # created to login. Enable the example_bash_operator dag in the home page
   ```



## 使用

```
export AIRFLOW_HOME=~/airflow

airflow webserver --port 8080

airflow scheduler
```



## 核心概念

### DAG 图

DAG图即有向无环图(Directed Acyclic Graph)，将所有需要运行的tasks按照依赖关系组织起来, 描述的是一个工作流的过程。

DAG 不关心里面的任务做了什么事情，而是关心

- 任务在特定的时间开始
- 若干任务以正确的顺序进行
- 对未期望的情况有正确的处理

### Operators

DAG定义了一个工作流，operators定义了工作流中的每一task具体做什么事情。一个operator定义工作流中一个task，每个operator是独立执行的，不需要和其他的operator共享信息。它们可以分别在不同的机器上执行。

如果你真的需要在两个operator之间共享信息，可以使用airflow提供的Xcom功能。

BashOperator - executes a bash command 

PythonOperator - calls an arbitrary Python function 

DummyOperator：空操作（测试时占位或者分支时跳过某些task）

https://stackoverflow.com/questions/57481237/use-case-of-dummy-operator

EmailOperator - sends an email 

HTTPOperator - sends an HTTP request 

SqlOperator - executes a SQL command 

Sensor - waits for a certain time, file, database row, S3 key, etc… 

### Tasks

Task为DAG中具体的作业任务，依赖于DAG，也就是必须存在于某个DAG中。

Task在DAG中可以配置依赖关系（当然也可以配置跨DAG依赖，但是并不推荐。跨DAG依赖会导致DAG图的直观性降低，并给依赖管理带来麻烦）。

## 作用

- 管理任务依赖
- 调度任务工作流
- 监视任务执行状态。

## 特点

1、分布式任务调度: 允许一个工作流的不同的 task 在多台 worker 上同时执行（需要CeleryExecutor）

2、可构建任务依赖: 以有向无环图的方式构建任务依赖关系;

3、task 原子性: 工作流上每个 task 都是原子可重试的, 一个工作流某个环节的 task 失败可自动或手动进行重试, 不必从头开始任务;

## 架构

在一个可扩展的生产环境中，Airflow通常含有以下组件：

元数据库：这个数据库存储有关任务状态的信息。

调度器：Scheduler 是一种使用 DAG 定义结合元数据中的任务状态来决定哪些任务需要被执行以及任务执行优先级的过程。调度器通常作为服务运行。

执行器：Executor 是一个消息队列进程，它被绑定到调度器中，用于确定实际执行每个任务计划的工作进程。有不同类型的执行器，每个执行器都使用一个指定工作进程的类来执行任务。例如，LocalExecutor 使用与调度器进程在同一台机器上运行的并行进程执行任务。     其他像 CeleryExecutor 的执行器使用存在于独立的工作机器集群中的工作进程执行任务。

Workers：这些是实际执行任务逻辑的进程，由正在使用的执行器确定。

![img](https://i.loli.net/2021/05/18/pU5dyzcP6L3BtSY.jpg)



### scheduler

scheduler的逻辑：

1. 遍历DAG路径下的所有dag文件
2. 启动一定数量的进程（进程池），并且给每个进程指派一个dag文件。每个进程解析分配给它的dag文件，并根据解析结果在DB中创建DagRun和TaskInstance（可在数据库中查看表内容）。对于满足执行条件的TaskInstance，将状态修改为SCHEDULED
3. 在scheduler的主循环中，查询状态为SCHEDULED的TaskInstance，并将这个TI发送给executor异步执行。至于怎么执行scheduler就不管了，只需要从executor同步状态信息。
4. 在进程池中如果有进程完成了，则创建新的进程处理下一个dag文件，并且保证这个进程池的进程数量不会超过配置的数量。
5. 一旦所有的dag处理完毕后，就会进行下一轮循环处理。这里还有一个细节就是上一轮的某个dag的处理时间可能很长，导致到下一轮处理的时候这个dag还没有处理完成。Airflow的处理逻辑是在这一轮不为这个dag创建进程，这样不会阻塞进程去处理其余dag。



### Executor

Worker的具体实现由配置文件中的`executor`来指定，airflow支持多种`Executor`:

- SequentialExecutor: 单进程顺序执行，一般只用来测试
- LocalExecutor: 本地多进程执行
- CeleryExecutor: 使用[Celery](https://docs.celeryproject.org/en/stable/)进行分布式任务调度
- DaskExecutor：使用[Dask](https://distributed.dask.org/en/latest/)进行分布式任务调度
- KubernetesExecutor: 1.10.0新增, 创建临时POD执行每次任务

其中常用的是CeleryExecutor 和 KubernetesExecutor。 这里介绍下LocalExecutor 和 CeleryExecutor 分别代表单机和分布式模式。

- **分布式模式**

1、Schedual读取配置文件 将Job信息发给RabbitMQ， 并在数据库里注册Job信息

2、RabbitMQ里有很多channel， schedual根据Job信息 发到对应的channel

3、Executor会被配置为 Celery Executor（在 airflow.cfg 中配置），并且指向 RabbitMQ Broker， 消费RabbitMQ对应的channel。

4、Worker 被安装在不同的节点上，它们从 RabbitMQ Broker 中读取任务，并执行，最终将结果写入数据库。

5、Web读取MySQL里面的Job信息，展示Job的执行结果

- 单机模式

### xcom

XComs(cross-communication)使得任务之间可以交换信息，允许更细粒度的控制和状态共享。

Task可以在运行时通过`xcom_push(key, value)`发送任意**可序列化成JSON**的对象。

Task中也可以通过`xcom_pull(task_id(s), key)`获取到一个或多个task的xcom值。

## 第一个Dag文件

https://www.applydatascience.com/airflow/writing-your-first-pipeline/

- Step 1: Importing modules
- Step 2: Default Arguments
- Step 3: Instantiate a DAG
- Step 4: Tasks
- Step 5: Setting up Dependencies

```python

#第一步 导入模块
from datetime import timedelta

# The DAG object; we'll need this to instantiate a DAG
from airflow import DAG

# Operators; we need this to operate!
from airflow.operators.bash import BashOperator
from airflow.utils.dates import days_ago


# 第二步 设置默认参数
# These args will get passed on to each operator
# You can override them on a per-task basis during operator initialization
default_args = {
    'owner': 'airflow',
    'depends_on_past': False,
    'email': ['airflow@example.com'],
    'email_on_failure': False,
    'email_on_retry': False,
    'retries': 1,
    'retry_delay': timedelta(minutes=5),
    # 'queue': 'bash_queue',
    # 'pool': 'backfill',
    # 'priority_weight': 10,
    # 'end_date': datetime(2016, 1, 1),
    # 'wait_for_downstream': False,
    # 'dag': dag,
    # 'sla': timedelta(hours=2),
    # 'execution_timeout': timedelta(seconds=300),
    # 'on_failure_callback': some_function,
    # 'on_success_callback': some_other_function,
    # 'on_retry_callback': another_function,
    # 'sla_miss_callback': yet_another_function,
    # 'trigger_rule': 'all_success'
}


# 第三步 实例化dag对象，第一个参数为id，区分不同的dag
dag = DAG(
    'first_dag_file',
    default_args=default_args,
    description='A simple tutorial DAG',
    schedule_interval=timedelta(days=1),
    start_date=days_ago(2),
    #可在ui界面根据tag进行筛选
    tags=['first,example'],
)

# 第四步 构建任务（t1,t2,t3）
# t1, t2 and t3 are examples of tasks created by instantiating operators
t1 = BashOperator(
    task_id='print_date',
    bash_command='date',
    dag=dag,
)

t2 = BashOperator(
    task_id='sleep',
    depends_on_past=False,
    bash_command='sleep 5',
    retries=3,
    dag=dag,
)
dag.doc_md = __doc__

t1.doc_md = """\
#### Task Documentation
You can document your task using the attributes `doc_md` (markdown),
`doc` (plain text), `doc_rst`, `doc_json`, `doc_yaml` which gets
rendered in the UI's Task Instance Details page.
![img](http://montcs.bloomu.edu/~bobmon/Semesters/2012-01/491/import%20soul.png)
"""
#具体模板、宏定义参考链接 https://airflow.apache.org/docs/apache-airflow/stable/macros-ref.html
#{{ ds }} ----->>>the execution date as YYYY-MM-DD
#airflow.macros.ds_add(ds, days)---->>>Add or subtract days from a YYYY-MM-DD

templated_command = """
{% for i in range(5) %}
    echo "{{ ds }}"
    echo "{{ macros.ds_add(ds, 7)}}"
    echo "{{ params.my_param }}"
{% endfor %}
"""

t3 = BashOperator(
    task_id='templated',
    depends_on_past=False,
    bash_command=templated_command,
    # 参数为字典
    params={
      				'my_param': 'Parameter I passed in',
      				'key1':'value1',
      				'key2':'value2',
           },
    dag=dag,
)

# 第五步，设置任务的依赖关系
# 设置任务的依赖关系
"""
t1.set_downstream([t2, t3])
t1 >> [t2, t3]
[t2, t3] << t1

上面三种写法等效
"""
t1 >> [t2, t3]
```



## 执行Dag文件

​      1 python first_tutorial.py(first_tutorial.py为上面新建的dag文件)

​        执行完成后不提示错误即说明代码正确

​     2 打开浏览器界面，开始执行

注：需要webserver先成功运行

## schedule_interval

Here is a couple of options you can use for your `schedule_interval`. You can choose to use some preset argument or cron-like argument:

| preset     | meaning                                                      | cron        |
| :--------- | :----------------------------------------------------------- | :---------- |
| `None`     | Don’t schedule, use for exclusively “externally triggered” DAGs |             |
| `@once`    | Schedule once and only once                                  |             |
| `@hourly`  | Run once an hour at the beginning of the hour                | `0 * * * *` |
| `@daily`   | Run once a day at midnight                                   | `0 0 * * *` |
| `@weekly`  | Run once a week at midnight on Sunday morning                | `0 0 * * 0` |
| `@monthly` | Run once a month at midnight of the first day of the month   | `0 0 1 * *` |
| `@yearly`  | Run once a year at midnight of January 1                     | `0 0 1 1 *` |

**Example usage**:

- Daily schedule:
  - `schedule_interval='@daily'`
  - `schedule_interval='0 0 * * *'`



## 源码解析

### 参考链接

https://blog.csdn.net/wwyzxb/article/details/111148882

![在这里插入图片描述](airflow/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3d3eXp4Yg==,size_16,color_FFFFFF,t_70.png)

![在这里插入图片描述](airflow/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3d3eXp4Yg==,size_16,color_FFFFFF,t_70-20210520145222630.png)

循环的主要步骤如下：

通过DagFileProcessorAgent获取DAG文件解析结果

查找并排队可执行的任务

改变DB中的tis状态;
在执行器中对任务进行排队
心跳执行器

在执行器中异步执行排队的任务（调用executor的trigger_tasks方法）
同步运行任务的状态（调用sync方法同步任务执行状态）

## FAQ

1 sqlite不呢并行执行task，需要mysql或者postgresql？

sqlite是基于文件的，多线程不能同时写入，mysql和postgresql是基于客户端和服务端的，支持多线程

三种数据库比较可参考链接：

https://logz.io/blog/relational-database-comparison/