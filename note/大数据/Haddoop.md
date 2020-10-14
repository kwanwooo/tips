# Hadoop

Hadoop是Apache旗下的适合大数据的分布式存储和计算平台

## 核心组件

Distributed File System（HDFS）、MapReduce和YARN

## 版本

- Apache
- Cloudera（CDH、稳定，基础版本免费，使用较多）
- Hortonworks（HDP）
- IBM定制
- Intel定制
- 华为定制

## 生态圈

- Flume Sqoop
	- Zookeeper
- H Y Oozie
- D A Pig
- F R Mahout
- S N RConnectors
    - Hive
    - Hbase

## 分布式和集群区别

- 集群：同一个业务，部署在多个服务器上， 干同一件事的多个人称之为集群
- 分布式：一个业务分拆多个子业务，部署在不同的服务器上， 把一件事分成多个部分给不同人做，称之为分布式

## 主要模块

- Common 为其他Hadoop模块提供基础设施
- HDFS 高可用、高吞吐量的分布式文件系统
- MapReduce 分布式离线并行计算框架
- YARN 新的MapReduce框架，任务调度与资源管理

## 优点

- 可靠（多个副本）
- 可拓展（支持拓展）

## 块：128Mb(默认)

- 100Mb->100Mb
- 150Mb->128Mb+22Mb
- 100Mb+150Mb->100Mb+128Mb+22Mb

## 分布式架构

- 主从架构master/slavers->

    - NameNode:主节点 存储管理元数据（内存）（元数据指数据的名称，副本数，位置，权限等）
    - DataNode:从节点 存储数据消耗机器上的磁盘
    - SecondaryNameNodeameNode 同步元数据和日志
    - DFSClient
    - 客户端

- 主从架构处理逻辑

    - 写操作：客户端发请求->namenode->写入操作
    - 读操作：客户端发请求->namenode指定位置->就近获取数据
    - 读写通过RPC协议途径交流
    - HDFS的设计理念：一次写入（单个用户）、多次读取（不能修改）

## YARN

- 客户端提交任务
- 主节点NameNode通知应用管理者AppMstr
- 应用管理者切分数据，申请资源
- 主节点NameNode分配容器
- 任务运行
    1. 成功：应用管理者向主节点反馈信息，释放资源，关闭任务
    2. 失败：应用管理者重新提交申请资源，重新分配资源
	
