# Elasticsearch 概念

- Cluster 集群
**集群通过一个唯一名字来识别** 默认是的是“elasticsearch”，集群节点（Node）通过_集群的名字（cluster name）_来加入集群。

- Node（节点）

集群下的单个节点服务器，存储数据参与集群的索引(indexing)搜索工作(search),主要也是通过名字（name）来识别。每个节点（node）通过配置集群名字（cluster name）来加入一个指定的集群，默认的都是加入elasticsearch的集群。

- index
索引是一系列有相似属性数据组成的文档（Documents）

- Type
在索引内，可以定义一个或者跟多的类型。
一个类型（Type）是逻辑分类、分区。

- Document     

在索引、类型中可以存储很多你想要的文档

- 集群 复制

[集群配置参考地址](http://www.wklken.me/posts/2016/06/29/deploy-es.html)


# 插件安装方式
```
./plugin install mobz/elasticsearch-head
```

##查看集群的运行状态接口
```
curl 'localhost:9200/_cat/health?v'

epoch      timestamp cluster       status node.total node.data shards pri relo init unassign
1394735289 14:28:09  elasticsearch green           1         1      0   0    0    0        0
```

## 查看集群下的节点（node）

```
curl 'localhost:9200/_cat/nodes?v'

host         ip        heap.percent ram.percent load node.role master name
mwubuntu1    127.0.1.1            8           4 0.00 d         *      New Goblin

192.168.8.17  192.168.8.17  7 99 2.47 d * node-1               
192.168.8.186 192.168.8.186 2 16 0.00 d m node-elasticsearch-2 
```
##查看所有的索引

```
curl 'localhost:9200/_cat/indices?v'

green open jonas    5 1    0 0  1.5kb   800b 
green open .kibana  1 1    6 1 60.1kb   30kb 
green open applog   5 1 8911 0    5mb  2.5mb 
green open index    5 1    0 0  1.5kb   795b 
green open blog     5 1    1 0  8.1kb    4kb 
green open users    5 1   22 1 58.5kb 29.2kb 
green open customer 5 1    0 0  1.5kb   800b 
```

## 创建一个索引
```
curl -XPUT 'localhost:9200/customer?pretty'
curl 'localhost:9200/_cat/indices?v'
```

##增加数据
localhost:9200/[index]/[type]/[id]

```
curl -XPUT 'localhost:9200/customer/external/1?pretty' -d '
{
  "name": "John Doe"
}'

```

## 删除一个索引

```
curl -XDELETE 'localhost:9200/customer?pretty'
curl 'localhost:9200/_cat/indices?v'
```

## 修改索引文档

```
curl -XPUT 'localhost:9200/customer/external/1?pretty' -d '
{
  "name": "Jane Doe"
}'
```

## 修改文档（Document）

```
curl -XPOST 'localhost:9200/customer/external/1/_update?pretty' -d '
{
  "doc": { "name": "Jane Doe" }
}'

// This example shows how to update our previous document (ID of 1) by changing the name field to "Jane Doe" and at the same time add an age field to it:

curl -XPOST 'localhost:9200/customer/external/1/_update?pretty' -d '
{
  "doc": { "name": "Jane Doe", "age": 20 }
}'

```

## 删除 文档（Document）

```
curl -XDELETE 'localhost:9200/customer/external/2?pretty'
```

## 批量处理(Batch Processingl)

```
curl -XPOST 'localhost:9200/customer/external/_bulk?pretty' -d '
{"index":{"_id":"1"}}
{"name": "John Doe" }
{"index":{"_id":"2"}}
{"name": "Jane Doe" }
'
```


#搜索

两种基本的搜索方式

-   通过restAPI发送搜索字段
- 发送restBody

>发送参数的方式
>curl 'localhost:9200/bank/_search?q=*&pretty'
>发送body的查询方式
>curl -XPOST 'localhost:9200/bank/_search?pretty' -d '
{
  "query": { "match_all": {} }
}'

