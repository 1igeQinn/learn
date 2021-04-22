# MongoDb 增加管理员


```
db.createUser(
   {
     user: "liwuyue",
     pwd: "liwuyue1234",
     roles:
       [
         { role: "readWrite", db: "config" },
         "clusterAdmin"
       ]
   }
)
```

[doc](https://docs.mongodb.com/manual/reference/method/db.createUser/#create-administrative-user-with-roles)
