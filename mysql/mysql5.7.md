# MySQL 5.7 data type of Json

##创建一个支持json的表

```
create table user1 ( 
	uid int auto_increment,  
	data1 json,
	primary key(uid)
	);
	
	// 插入数据
	insert into user1 values (NULL,'{"name":"David","mail":"jiangchengyao@gmail.com","address":"Shangahai"}');
     
   // 查询json中的值
select JSON_EXTRACT(data1, '$.name'),JSON_EXTRACT(data1,'$.address') from user1;
```


