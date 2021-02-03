##概念
- NRT（近乎实时） 最多延迟1s 查询
- 集群
每个集群被一个唯一的名字所标识 默认是'elasticsearch'
node 节点
集群下的单个服务器，保存数据

index 索引
索引的名字（标识） 必须小写

- Type 


## 操作
修改（指定）节点名称
./elasticsearch --cluster.name my_cluster_name --node.name my_node_name

# 查看cluster Health 信息
curl 'localhost:9200/_cat/health?v'

# 列出所有的（indices）目录
curl 'localhost:9200/_cat/indices?v'

#创建索引

curl -XPUT 'localhost:9200/customer?pretty'
curl 'localhost:9200/_cat/indices?v'

删除索引
curl -XDELETE 'localhost:9200/customer?pretty'
curl 'localhost:9200/_cat/indices?v'

修改数据

curl -XPUT 'localhost:9200/customer/external/1?pretty' -d '
{
  "name": "John Doe"
}