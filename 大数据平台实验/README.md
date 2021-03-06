﻿# 实验归纳  

## 1.实验镜像使用
实验过程中主要制作了两个镜像:  

demo_3 hadoop-spark集成镜像:  
1.JDK 1.8  
2.hadoop 2.7.2  
3.scala 2.12.2  
4.spark 2.1.0 

镜像大小:1.99G
使用方法: /etc/profile文件已经修改，启动集群后最好先source /etc/profile，然后根据需要启动hadoop或spark  

demo_4 storm镜像:  
1.JDK 1.8  
2.zookeeper 3.4.10  
3.storm 1.1.0  

镜像大小:1.17G
使用方法: 启动脚本都已经放在根目录，先启动zookeeper，再启动storm  

实验过程中使用过的hadoop生态圈的组件像是Hive,HBase还没有集成进这些镜像里，到时若需要使用可改进这些镜像。  

## 2.提醒  
我个人在实验过程中是demo2,demo3,demo4镜像都有拿来做实验的。  

实验1~12 当时我都是在demo2上完成的，但是demo2 JDK版本比较旧，然后也没安装vim(vi特别不好用), 推荐的话还是用demo3去完成实验。  

实验13~19 做到这里要频繁使用spark，就编写了Dockerfile 写了demo3的镜像，可以直接用。  

实验24~25 用到storm，可以直接使用demo4完成实验。  

其他一些部件，像是Hive,HBase,Flume,Karfa,Pig,MongoDB等我都只是在demo3镜像创建的集群的master节点上安装并实验了一遍，并没有保留或写成Dockerfile(之后如果有需要的话可以完善Dockerfile)。

## 3.实验中遇到的问题  

### **实验1~4:**   
比较基础，没有太大问题，比较不好理解的是实验4的Distributed shell  

### **实验5~9:**  
都是mapreduce实验，都是需要实际进行代码编写,如果用javac命令进行编译要注意修改/etc/profile的CLASSPATH部分，实验中也有讲到。  

如果用开发工具的话，注意要导入hadoop里的一些jar包,一直只要用到两个jar包:  
hadoop-common-2.7.2.jar, hadoop-mapreduce-client-core-2.7.2.jar  
**common jar包在/usr/local/hadoop/share/hadoop/common/目录下  
mapreduce jar包在/usr/local/hadoop/share/hadoop/mapreduce/目录下**  

代码上的话实验6跟实验8代码比较难理解，实验8实验结果也一直有乱码出现(个人觉得代码上应该是没有错误的)  

### **实验10~12:**   
Hive实验部分,主要是安装部署和一些基本操作。  

Hive的部署主要有三种模式:  
**1.内嵌模式:** 元数据保存在内嵌的derby中（使用很不方便）,quit退出交互之后操作记录并不会保存。  
**2.本地模式:** 本地安装mysql,替代derby存储元数据, 本地模式的安装还算比较简单( 参考写的文档Hive本地模式部署)，能成功连接上。远程安装mysql（即在别的主机上安装mysql并连接就会出现问题，尝试过创建mysql容器去部署本地模式，但最后结果是连接不上mysql)  
**3.远程模式:** hive服务和metastore在不同的进程内，可能是不同的机器。（这部分没有去实验过，不太了解）  

### **实验13~19:**   
均是Spark实验，实验13~16比较简单，都是一些比较简单的基础操作。实验17~19就出现了不少问题。  

首先Spark有两种启动模式，单机模式和集群模式。  

**实验17是Spark SQL**: 原先实验是要求在集群模式下启动的，前面的操作都正常，到查询数据那就会报错，无法获取先前插入的数据，原因不明。  
**实验18是Spark Streaming**: 安装原实验进行操作无法获得相应的实验结果，有错误。但是运行Spark自带的Spark Streaming例子则可以成功运行。  
**实验19是GraphX**: 代码比较复杂，且无法运行jar包！  

### **实验20~21:**  
zookeeper的安装部署和一些基本操作，实验内容比较简单。  

### **实验22~23:**  
HBase实验，实验内容比较简单，就是安装部署和一些简单使用，**唯一要注意的比较奇怪的点是在实验22里使用HBase Shell时如果事先没有修改/etc/hosts文件添加主机域名的映射会无法正常使用**。  

### **实验24~25:**  
Storm实验，因为storm跟hadoop,spark没有什么关系，所以单独制作了镜像demo4。  
实验内容也不是很复杂，跟着实验去做即可。  

### **实验26~28:**  
都是一些组件的安装部署和简单使用。  

实验26: Flume  实验27: Kafka 实验28: Pig  

### **实验29~30:**  
Redis实验，安装需要用make命令进行编译。实验不复杂。  

### **实验31~32:** 
两个数据库,MongoDB和LevelDB，实验过程没有遇到太多问题，就是对这两个数据库比较陌生。  

### **实验33~36:**  
都涉及到机器学习。
实验33 Mahout 是通过hadoop进行一些机器学习任务。 
实验34~36 是spark 自带的机器学习库Mllib，机器学习部分我了解得不多，所以只是按实验操作实验了一遍，具体效果不清楚。  









