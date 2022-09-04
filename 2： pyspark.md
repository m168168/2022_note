# 1： pyspark

~~~python
https://www.bilibili.com/video/BV1j4411u7hT?p=6&spm_id_from=pageDriver
spark core 
spark sql
spark streaming 
spark MLlib
图计算 GraphX 

spark + yarm + hdfs  
spark + mysql redis kafka zookeeper 
部署模式：
local 
至少2台
standalone 自带集群模式
yarm   集群模式
mesos  集群模式 

master  worker 
1：配置主节点 到从节点免登录 
2： 关闭防火墙  （大数据都是内网集群）
service iptables status
serverice iptables stop
chkconfig iptables off
3: IP 和hostname 映射关系
ip hostname

spark 目录：
bin   可执行的脚步
conf   配置文件
jars   依赖jar 包
sbin   集群管理命令

修改配置文件：
spark-env.sh
export JAVA_HOME=
export SPARK_MASTER_HoST=hdp-01
export SPARK_MASTER_PORT=7077
7077: 是spark 内部通信端口  worker向master 连接端口
8088： web 访问master 的端口  
slaves.sh
hdp-02/ip  所有的从节点 

# 分发安装包
for i in 2 3 4;
do scp -r spark(安装包)/ hdp-0$i:$PWD ; done 

# 启动
start-master.sh
start-slavers.sh
start-all.sh
# 日志问题
spark-home/logs

master 启动命令 
java -cp *** **.class 参数列表
netstat -natpl | grep 1608

在spark  hadoop  都有start-all.sh 
 /etc/profile  谁先加载 ，谁生效 ，  或者改名 

启动后 : master 地址：  spark://hdp-01:7077 

work 占用资源： 
cores  : 当前机器
memory  ： 当前机器 内存-1g

# spark 提交任务
客服端：
1必须安装spark 安装包 spark-submit
2必须连接到master
spark 提交给maset ,在集群执行

spark-shell : 交互式命令行
spark-submit : 标准的提交命令
    
spark-submit 选项 jar包 参数列表

--master   yarm spark://host:port local  默认local   local[*] 可以指定核
--class  主方法所在类
--deploy-model  driver 位置  driver的位置
clinet  : driver 运行在客服端
cluster : driver 在集群中的某一台 
jar 架包

在写spark 程序的时候必须有sparkContext
在集群模式下， 不能读取本地的文件 一般读取hdfs 文件 

1: master 先启动 ，检查超时的worker
2： worker 启动 向 master 注册 ， 资源信息 （memory ,core）
3: master 保存worker的相关信息
4： master 向worker 发送注册成功的消息
5： worker 启动定时任务， 报活  ，发送心跳
5: master 修改worker的最后一次心跳时间
    
1:客户端请求application 
2:master 进行资源分配
   打散策略
  每一个空闲的worker 来参与运行任务，向worker 发送指令 ，启动executor
3: driver :
	解析业务逻辑功能
	切分阶段 stage
	创建task ,条件task  （task 执行的最小单位）
4: excutor 向driver 注册 ，并通信
    

常驻进程：
master ： 集群的管理者， 管理worker , 负责客服端的任务请求调度
worker : 向master 通信 ，管理自己的executor
任务执行时：
在哪里提交，在哪里产生 sparksubmit 进程
coarseGrainedExecutorBackend 提供干活的资源 简称executor 所有的task
driver程序： 主控程序 ， 解析业务逻辑代码， 切分阶段stage 创建task 提交task 到executor执行

可以指定资源分配：
--executor-cores  每一个executors（work） 占用的cores
--executor-memory    每一个executors 占用的memory
--total-executor-cores  application 能使用的最多cores数

work  : 启动
    
在提交spark 任务，反射执行自定义main方法
1： 客服端提交 spark-submit 选项 jar包 参数列表
2: 调用spark-class 脚本 通过exec 执行启动一个main方法
3： SparkSubmit.main 反射执行一个类 wordCount.main 
4: new SparkContext 
    创建3个核心的对象 TaskScheduler , DAGScheduler ,SchedulerBackend
SchedulerBackend : coarseGrainedExecutorBackend , StandaloneSchedulerBackend
~~~



~~~
分为两类算法：
Transfomer : 转换算子 lazy  产生一个新的rdd
map fliter flatMap goupBykey reduceBykey aggregateByKey ,union ,join ,coalesce
action :    执行 (写文件 ， ) 返回结果给驱动程序 ，或写入文件系统
reduce ,collect ,count  ,first ,take ,countByKey , foreach 

产生job 

Application ->job（DAG）->Stage -> task 
RDD: 弹性分布式数据集合  resillebt distributed dataset（不可变得 ，只读的）
弹性： 容错能力 
分布式： 以分区为单位 ，运行在不同的节点上

1: rdd 的创建：
集合并行化
读取外部系统文件  sc.textFilxt(path)
转换算子
2:  rdd 的分区  默认分区数量 = application 使用的cores 数量
 每一个rdd 都有分区 。 rdd.size 分区的数量
partition :  
hdfs :   分区数量 = 读取hdfs 文件的block 快的数量


RDD依赖关系  父到子
宽依赖  有shuffle操作
窄依赖 
划分阶段
从计算过程：
ont-to-one  所有作业可以流水线  pipeline 速度快 窄依赖
宽依赖必须拿到所有分区的数据才能计算，速度慢
容错： 窄依赖 好 宽依赖差

基于以上2点， 用dependency , 用于封装两种不同的依赖关系  ，然后搞出stage阶段
把所有的窄依赖放在一个阶段中 

窄依赖算子：
map flatMap filter 不会改变分区数量
union coalesce   增加  减少分区数量
所有的窄依赖算子rdd 都在一个阶段中 stage
（一旦遇到宽依赖 ，就切分stage）
宽依赖算子: shuffle 一对多的关系  : 有几个算子 就切分多个阶段
groupByKey  reduceByKey distinct 

Stage ： spark 中对所有的窄依赖的封装 ，提供的一个抽象类
Stage： ResultStage ： 只有一个 ， 就是最后一个stage
ShuffleMapStage :  0 到多个

Stage 是有起始边界：
ShuffleMapStage： 起点  job 中的第一个RDD
					终点： shuffle Write
ResultStage:  起点: Shffle Read 
				终点： job 中最后一个RDD 
job的起始位置：
当触发action 算法的时候，产生job  ， job终止位置 ,就是action算子对应的RDD
~~~



~~~
DAG ： 有向五环图
有向： 数据的流向， RDD的依赖方向
无环 ： 不是闭环
图：  点 RDD  线 rdd 之间的依赖关系 

1Driver 
在解析业务逻辑代码的时候 ，完成DAG的构建，当触发action 算子的时候，DAG构建完成
2DAGSchedule
基于DAG,切分stage ，创建task ，提交stage
3Taskschedule
调度Task ，提交task 给executor 执行 




~~~



### 基本算子

~~~
map :  一一映射  对每一条数据执行
mapValues :
mapPartitions: 一一映射,对每个分区 
mapPatitionWithIndex

zip  分区数量必须一致，每个分区的元素也必须一致   a ,b ->（a, b）
zipWithIndex 

groupByKey 
默认的分区器 ：  key hashcode % 分区数
数据重新分发 ： shuffle 
reduceByKey
分区类聚合  
能使用reduceByKey 就不用groupByKey  

foreach  一一映射 ， 没有返回值 ， 常见的打印  每次迭代一个元素  
foreachPartition 

sortByKey   产生 job
zipWithIndex  产生 job
take 产生 job
reduct 元素并归 ， 没有顺序
coutByKey    某个元素的key 的个数
collectAsMAp  ： 用于[k,v] rdd , 以map 集合返回
take()
first()
top()  返回前n 个
takeOrdered(n) 

~~~

### RDD的高级应用 

~~~
1：RDD 的缓存和持久化 
默认情况下， 每一个action 操作 ， 都会重新计算上面的转换RDD （重新计算）
如果能把该RDD的结果缓存下来， 那么基于该RDD的操作，就不需要从头计算 
cache() (StoregeLevel )  缓存
persisit(StoregeLevel.MeMORY_AND_DISK) 持久化
执行完业务逻辑，可以手动释放
unpersisit()

2：RDD 的checkpoint 容错方案 
把rdd 中的数据 ，写到分布式文件系统中
sc.setCheckpointDir('hdfs://ip:port/dir')
rdd.checkpoint   
	1:是lazy 算子  ，当触发action算子的时候， 才执行，产生2个job,第一个job	
是 执行业务逻辑， 第二个job 执行写入到数据到hdfs
	2: 当对某一个rdd 执行checkpoint 之后， 该RDD原有的父依赖关系被删除 ，取而代之是checkpointRDD
	3: 以后对该RDD所有的操作，依赖关系从CheckpointRDD开始，真正的数据从hdfs 读取
	
在特别复杂的业务逻辑中，才会用 	

3： RDD 中的共享变量（广播变量 ， 累计器） 广播大变量  在driver端一个副本 

RDD的内存管理方法：
spark1.x 静态内存管理 （各个模块的占比是固定的 ，容易造成不均衡 淘汰）
spark2.x 统一的内存管理  

内存的组成部分：
总的内存 = 系统预留内存（300M） + 可用内存
可用内存  = 统一内存（0.6） + 其他（0.4）
统一内存 = 存储内存(storege)（0.5） + 执行内存 (executiom)（0.5）

Storege 存储内存 ：
缓存RDD ,展开partition ,存放Direct task result ，存放广播变量 ，在spark Streaming reciver 模式中， 存放每个batch 的blocks
execution 执行内存：
用于shuffle , join , sort ,aggregation(聚合) ，buffer等操作
其他：
spark : 内部的元数据 ， OOM错误 ， 

默认配置参数， spark.memory.fraction = 0.6
			 spark.memory.storageFraction=0.5
			 

Torrent 比特洪流技术
广播变量实现类 ： TorrentBroadcast 
利用广播变量， 能保证一个executor的所有task 共用一份反序列化的数据
减少数据的反序列化和GC
使用：
    diver 端广播  blockManagerMaster 
    executor 使用  blockManager 
注意使用： 
1除了RDD 不能被广播， 其他的类 、集合。对象都可以被广播
2： 被广播数据， 可以在任意的executor 中通过value调用
3： 广播变量是只读的，不能被修改 
4： 最大的功能是，就是保证一个executor中所有的task共用一份数据 ，提升效率 


4： 累加器
在driver端定义一个类加器
全局的 可以通过Web 监控界面查看 
acc = sc.LongAccumulator('variable_acc')

总结：
1在driver端定义累加器
2在任意的函数中，executor中通过add方法调用
3累加器是全局(application为单位)的累加 
4在driver端 ，通过value 方法获取值
5在程序的监控界面，通过累加器的名称来获取值

~~~

### spark 的序列化

~~~
spark 中使用的序列化机制 默认是java 序列化 javaSerializer
内存中对象  序列化 二进制文件  网络传输 反序列化

KryoSerializer  : 占用内存少，速度快， 需要注册

1： spark standalone HA  （high avaliable ） 高可用  7 * 24  (集群) 
 单点故障  核心节点
 standlone master worker
 master alive  master standby(热备)
zookeeper 管理节点 高可用 
2： spark on yarn  standalone 两套不同的集群

yarn 集群  
客服端提交任务  1台（满足条件  ，spark 安装包 ， hadoop 的配置 （hdfs  +yarn）） 连接到hadoop集群 

yarn 集群：
ResourceManager 
NodeManager
1: 修改 ${hadoop}/etc/hadoop/capacity-scheduler.xml 中的资源调度

2： yarn.site.xml


spark 的客服端配置 
1：jdk
vim ${spark_home}/conf/spark-env.sh
2: hadoop_conf_dir  /yarn_conf_dir # hadoop的配置文件路径 

spark-submit --master yarn --deploy-model client/cluster 

两种部署模式区别 ：
cluster : Driver 运行在集群中的某一个节点 ， Driver 可以容错 ，提交任务，就可以退出
client :  Driver 运行在客服端 
~~~





### UDF 自定义函数

~~~
第1种方式
# 定义自定义函数
 def fun_name():
 	pass
# 注册自定义函数
udf1 = functions.udf(fun_name, FloatType()
# 使用自定义函数
dataframe = dataframe.withColumn(col, udf1(col))
第2种方式
注册udf，在sql中使用
spark.udf.register("udf1", fun_name,StringType()) 
dataframe = dataframe.withColumn(col, udf1(col))
第3种方式 注解形式更方便
@udf(returnType=StringType()) 
def fun_name():
 	pass
df.withColumn("Cureated Name", convertCase(col("Name"))).show(truncate=False)

pandas_udf函数支持定义三种类型的函数，分别为SCALAR、GROUP_MAP、GROUP_AGG，在pyspark.sql.function.PandasUDFType 中做了定义

from pyspark.sql.functions import pandas_udf, PandasUDFType
~~~





~~~
由于数据中某些字段包含 json 数据，因此直接使用 DataFrame 进行读取会出现分割错误，所以如果要创建 DataFrame，需要先直接读取文件生成 RDD，再将 RDD 转为 DataFrame。过程中，使用 python3 中的 csv 模块对数据进行解析和转换。
~~~

~~~
https://zhuanlan.zhihu.com/p/349664650
RDD：代表一个不可变的，可分区的，可被并行操作的数据元素集合
在进行spark 运算时，spark会创建一个DAG（有向无环图）来优化计算效率，并且在执行actions动作之前，spark绝不会开始实际的任务执行
transformation操作
action: 操作：
最起码有三种方式可以用于创建rdd：
可以从文本文件中读取从collections对象中创建（比如一串数字，字符，pairs），通过SparkContext.parallelize()从其他rdd中通过map,filter等函数创建
map()
mapValues() # 作用于键值对
reduceByKey( lambda x, y: x+y)

reduceByKey()
combineBykey()
groupBykey()
aggregateByKey()
sortByKey() 



~~~



~~~
from pyspark.sql.functions import udf
from pyspark.sql.types import BooleanType

valid_words = {"beauty", "runway"} # Define a list of valid words
filtered_df = df.filter(udf(lambda kwords: len(valid_words & set(kwords))>0, # Condition to identify if we have at least, 1 valid word
                                  BooleanType())(df.Keywords))
filtered_df.show()

df = spark.createDataFrame([[["apocalypse"]],[[None]],[["beauty","test"]],[["runway","beauty"]]]).toDF("testcol")
df.show()



~~~



~~~
df.printSchema()
df.withColumn()
df.withColumnRenamed()
df.sort(col_name1.asc() , col_name.desc())
df.gropuby().agg(sum(), ave(),..).where( col('name')> 100)  # agg 可以同时使用多个聚合函数
df.filter() # 选择 select
df.filter("city == 'beijing' and ctr > 0.2").show() 支持字符串 
dropna() 删除空行
explode（col_name） # 该行拆成多行

~~~

~~~
DataFrame 的函数
Action 操作
1、 collect() ,返回值是一个数组，返回dataframe集合所有的行
2、 collectAsList() 返回值是一个java类型的数组，返回dataframe集合所有的行
3、 count() 返回一个number类型的，返回dataframe集合的行数
4、 describe(cols: String*) 返回一个通过数学计算的类表值(count, mean, stddev, min, and max)，这个可以传多个参数，中间用逗号分隔，如果有字段为空，那么不参与运算，只这对数值类型的字段。例如df.describe("age", "height").show()
5、 first() 返回第一行 ，类型是row类型
6、 head() 返回第一行 ，类型是row类型
7、 head(n:Int)返回n行  ，类型是row 类型
8、 show()返回dataframe集合的值 默认是20行，返回类型是unit
9、 show(n:Int)返回n行，，返回值类型是unit
10、 table(n:Int) 返回n行  ，类型是row 类型

dataframe的基本操作
1、 cache()同步数据的内存
2、 columns 返回一个string类型的数组，返回值是所有列的名字
3、 dtypes返回一个string类型的二维数组，返回值是所有列的名字以及类型
4、 explan()打印执行计划  物理的
5、 explain(n:Boolean) 输入值为 false 或者true ，返回值是unit  默认是false ，如果输入true 将会打印 逻辑的和物理的
6、 isLocal 返回值是Boolean类型，如果允许模式是local返回true 否则返回false
7、 persist(newlevel:StorageLevel) 返回一个dataframe.this.type 输入存储模型类型
8、 printSchema() 打印出字段名称和类型 按照树状结构来打印
9、 registerTempTable(tablename:String) 返回Unit ，将df的对象只放在一张表里面，这个表随着对象的删除而删除了
10、 schema 返回structType 类型，将字段名称和类型按照结构体类型返回
11、 toDF()返回一个新的dataframe类型的
12、 toDF(colnames：String*)将参数中的几个字段返回一个新的dataframe类型的，
13、 unpersist() 返回dataframe.this.type 类型，去除模式中的数据
14、 unpersist(blocking:Boolean)返回dataframe.this.type类型 true 和unpersist是一样的作用false 是去除RDD

集成查询：
1、 agg(expers:column*) 返回dataframe类型 ，同数学计算求值
df.agg(max("age"), avg("salary"))
df.groupBy().agg(max("age"), avg("salary"))
2、 agg(exprs: Map[String, String])  返回dataframe类型 ，同数学计算求值 map类型的
df.agg(Map("age" -> "max", "salary" -> "avg"))
df.groupBy().agg(Map("age" -> "max", "salary" -> "avg"))
3、 agg(aggExpr: (String, String), aggExprs: (String, String)*)  返回dataframe类型 ，同数学计算求值
df.agg(Map("age" -> "max", "salary" -> "avg"))
df.groupBy().agg(Map("age" -> "max", "salary" -> "avg"))
4、 apply(colName: String) 返回column类型，捕获输入进去列的对象
5、 as(alias: String) 返回一个新的dataframe类型，就是原来的一个别名
6、 col(colName: String)  返回column类型，捕获输入进去列的对象
7、 cube(col1: String, cols: String*) 返回一个GroupedData类型，根据某些字段来汇总
8、 distinct 去重 返回一个dataframe类型
9、 drop(col: Column) 删除某列 返回dataframe类型
10、 dropDuplicates(colNames: Array[String]) 删除相同的列 返回一个dataframe
11、 except(other: DataFrame) 返回一个dataframe，返回在当前集合存在的在其他集合不存在的
12、 explode[A, B](inputColumn: String, outputColumn: String)(f: (A) ⇒ TraversableOnce[B])(implicit arg0: scala.reflect.api.JavaUniverse.TypeTag[B]) 返回值是dataframe类型，这个 将一个字段进行更多行的拆分
df.explode("name","names") {name :String=> name.split(" ")}.show();
将name字段根据空格来拆分，拆分的字段放在names里面
13、 filter(conditionExpr: String): 刷选部分数据，返回dataframe类型 df.filter("age>10").show();  df.filter(df("age")>10).show();   df.where(df("age")>10).show(); 都可以
14、 groupBy(col1: String, cols: String*) 根据某写字段来汇总返回groupedate类型   df.groupBy("age").agg(Map("age" ->"count")).show();df.groupBy("age").avg().show();都可以
15、 intersect(other: DataFrame) 返回一个dataframe，在2个dataframe都存在的元素
16、 join(right: DataFrame, joinExprs: Column, joinType: String)
一个是关联的dataframe，第二个关联的条件，第三个关联的类型：inner, outer, left_outer, right_outer, leftsemi
df.join(ds,df("name")===ds("name") and  df("age")===ds("age"),"outer").show();
17、 limit(n: Int) 返回dataframe类型  去n 条数据出来
18、 na: DataFrameNaFunctions ，可以调用dataframenafunctions的功能区做过滤 df.na.drop().show(); 删除为空的行
19、 orderBy(sortExprs: Column*) 做alise排序
20、 select(cols:string*) dataframe 做字段的刷选 df.select($"colA", $"colB" + 1)
21、 selectExpr(exprs: String*) 做字段的刷选 df.selectExpr("name","name as names","upper(name)","age+1").show();
22、 sort(sortExprs: Column*) 排序 df.sort(df("age").desc).show(); 默认是asc
23、 unionAll(other:Dataframe) 合并 df.unionAll(ds).show();
24、 withColumnRenamed(existingName: String, newName: String) 修改列表 df.withColumnRenamed("name","names").show();
25、 withColumn(colName: String, col: Column) 增加一列 df.withColumn("aa",df("name")).show();

~~~



~~~
pyspark.sql.functions里有许多常用的函数，可以满足日常绝大多数的数据处理需求
df.show()  df.count()  df.printSchema() df.columns df.dtypes
df.select()
df.age.alias('new_name','name')
df.filter() #筛选
F.lit() 增加常数列
df.drop_duplicates()
df.distinct()
df.drop('id') # 删除列
df.dropna(subset=['age', 'name'])  # 传入一个list，删除指定字段中存在缺失的记录
df.fillna({'age':10,'name':'abc'})  # 传一个dict进去，对指定的字段填充
df.groupby('name').agg(F.max(df['age']))

~~~

~~~
df.select(F.max(df.age))
df.select(F.min(df.age))
df.select(F.avg(df.age)) # 也可以用mean，一样的效果
df.select(F.countDistinct(df.age)) # 去重后统计
df.select(F.count(df.age)) # 直接统计，经试验，这个函数会去掉缺失值会再统计

from pyspark.sql import Window
df.withColumn("row_number", F.row_number().over(Window.partitionBy("a","b","c","d").orderBy("time"))).show() # row_number()函数

~~~



~~~
第二步：在命令行下 输入下面的命令来安装Gnome包。
# yum groupinstall "GNOME Desktop" "Graphical Administration Tools"
第三步：更新系统的运行级别。
# ln -sf /lib/systemd/system/runlevel5.target /etc/systemd/system/default.target
第四步：重启机器。启动默认进入图形界面。
# reboot

# mysql 
wget -i -c http://dev.mysql.com/get/mysql57-community-release-el7-10.noarch.rpm
yum -y install mysql57-community-release-el7-10.noarch.rpm
yum -y install mysql-community-server
systemctl start  mysqld.service
systemctl status mysqld.service
grep "password" /var/log/mysqld.log
mysql -uroot -p
ALTER USER 'root'@'localhost' IDENTIFIED BY 'new password';
grant all privileges on *.* to 'root'@'192.168.0.1' identified by 'password' with grant option;
firewall-cmd --zone=public --add-port=3306/tcp --permanent
~~~

# 2:hive

```

https://zhuanlan.zhihu.com/p/100163942
https://zhuanlan.zhihu.com/p/103413663

1：Hive 查询原理：
hive 其实是将hql转成MR程序
元数据 是hive 表的一些参数 不是hdfs 上的数据
在执行查询操作时 ,先从元数据库中找到 对应表对应的文件位置
通过 hive的解析器、编译器、优化器 执行器 将 sql 语句 转换成 MR 程序，运行在 Yarn 上，最终得到结果。
Hive 是将数据映射成数据库和一张张的表，库和表的元数据信息一般存在关系型数据库上（比如 MySQL）
Hive 本身并不提供数据的存储功能，数据一般都是存储在 HDFS 上的（对数据完整性、格式要求并不严格）
MetaStore：存储和管理Hive的元数据，使用关系数据库来保存元数据信息。


2： 内部表和外部表
内部表会移动数据到指定位置 ，将数据文件移动到默认位置，一般都是/usr/hive/warehouse/ 目录下
外部表不会移动数据，数据在哪就是哪
内部表删除，数据一起删除
外部表不会删除数据
工作中使用外部表做为数据映射，而统计出的结果一般多使用内部表，因为内部表仅仅用于储存结果或者关联，与 HDFS 数据无关。
desc formatted 表名即可查看。 是否内部表 外部表


分区表
动态分区
静态分区
分桶表 超大数据
分桶表一般在超大数据时才会使用，分桶将整个数据内容按某列属性值取hash值进行区分，具有相同hash值的数据进入到同一个文件中，意味着原本属于一个文件的数据经过分桶后会落到多个文件中。

倾斜表
临时表

复合数据类型：
Hive 中复合数据类型有 Array、Map、Struct 这三种

Array 代表数组，类型相同的数据
Map 映射 k--v 对
Struct 则存储类型不同的一组数据


CREATE (DATABASE|SCHEMA) [IF NOT EXISTS] database_name   --DATABASE|SCHEMA 是等价的
  [COMMENT database_comment] --数据库注释
  [LOCATION hdfs_path] --存储在 HDFS 上的位置
  [WITH DBPROPERTIES (property_name=property_value, ...)]; --指定额外属性
describe database hive_test;

#删除数据库
DROP (DATABASE|SCHEMA) [IF EXISTS] database_name [RESTRICT|CASCADE];


CREATE [TEMPORARY] [EXTERNAL] TABLE [IF NOT EXISTS] [db_name.]table_name     --表名
  [(col_name data_type [COMMENT col_comment],
    ... [constraint_specification])]  --列名 列数据类型
  [COMMENT table_comment]   --表描述
  [PARTITIONED BY (col_name data_type [COMMENT col_comment], ...)]  --分区表分区规则
  [
    CLUSTERED BY (col_name, col_name, ...) 
   [SORTED BY (col_name [ASC|DESC], ...)] INTO num_buckets BUCKETS
  ]  --分桶表分桶规则
  [SKEWED BY (col_name, col_name, ...) ON ((col_value, col_value, ...), (col_value, col_value, ...), ...)  
   [STORED AS DIRECTORIES] 
  ]  --指定倾斜列和值
  [
   [ROW FORMAT row_format]    
   [STORED AS file_format]
     | STORED BY 'storage.handler.class.name' [WITH SERDEPROPERTIES (...)]  
  ]  -- 指定行分隔符、存储文件格式或采用自定义存储格式
  [LOCATION hdfs_path]  -- 指定表的存储位置
  [TBLPROPERTIES (property_name=property_value, ...)]  --指定表的属性
  [AS select_statement];   --从查询结果创建表

# 通过查询建立表
CREATE TABLE emp_copy AS SELECT * FROM emp WHERE deptno='20';
CREATE [TEMPORARY] [EXTERNAL] TABLE [IF NOT EXISTS] [db_name.]table_name  --创建表表名
   LIKE existing_table_or_view_name  --被复制表的表名
   [LOCATION hdfs_path]; --存储位置
CREATE TEMPORARY EXTERNAL TABLE  IF NOT EXISTS  emp_co  LIKE emp

加载数据到表
load data local inpath "/usr/file/emp.txt" into table emp;
重命名表
ALTER TABLE table_name RENAME TO new_table_name;
修改列

查询结果插入表
INSERT OVERWRITE TABLE tablename1 [PARTITION (partcol1=val1, partcol2=val2 ...) [IF NOT EXISTS]]   
select_statement1 FROM from_statement;

INSERT INTO TABLE tablename1 [PARTITION (partcol1=val1, partcol2=val2 ...)] 
select_statement1 FROM from_statement


导出数据
INSERT OVERWRITE [LOCAL] DIRECTORY directory1
  [ROW FORMAT row_format] [STORED AS file_format] 
  SELECT ... FROM ...
 
# 累计窗口 函数
sum() over()
avg() over()
# 排序窗口函数
rank() over()
dense_rank() over()
row_number() over()

```

~~~~
#分列
split_col = f.split(business['categories'], ',')
# 重命名 过滤掉空的数据 
business = business.withColumn("categories", split_col).filter(business["city"] != "").dropna()
# 临时表
business.createOrReplaceTempView("business")
# 筛选出想要的列数据 
 b_etl = spark.sql("SELECT business_id, name, city, state, latitude, longitude, stars, review_count, is_open, categories, attributes FROM business").cache()
 
# 到某店到州的center  的距离 
outlier = spark.sql(
        "SELECT b1.business_id, SQRT(POWER(b1.latitude - b2.avg_lat, 2) + POWER(b1.longitude - b2.avg_long, 2)) \
        as dist FROM b_etl b1 INNER JOIN (SELECT state, AVG(latitude) as avg_lat, AVG(longitude) as avg_long \
        FROM b_etl GROUP BY state) b2 ON b1.state = b2.state ORDER BY dist DESC")

# 内连接 
joined = spark.sql("SELECT b.* FROM b_etl b INNER JOIN outlier o ON b.business_id = o.business_id WHERE o.dist<10")
# 将一[1,2,3] 拆成多行 explode
part_business = spark.sql("SELECT state, city, stars, review_count, explode(categories) AS category FROM business").cache()
#统计全部的类别  
spark.sql("SELECT COUNT(DISTINCT(new_category)) FROM part_business")

#top 10 business categories
spark.sql("SELECT new_category, COUNT(*) as freq FROM part_business GROUP BY new_category ORDER BY freq DESC")

print("## Top business categories - in every city")
spark.sql("SELECT city, new_category, COUNT(*) as freq FROM part_business GROUP BY city, new_category ORDER BY freq DESC")

 print("## Cities with most businesses")
spark.sql("SELECT city, COUNT(business_id) as no_of_busy FROM business GROUP BY city ORDER BY no_of_bus DESC")

#
# 
~~~~

~~~
df.toJSON()
df.toPandas()

~~~

