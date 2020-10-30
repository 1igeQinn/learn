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