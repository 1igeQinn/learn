# Permission

## 通配符权限

```
subject.isPermitted("queryPrinter")

//等价于
subject.isPermitted( new WildcardPermission("queryPrinter") )

```

 ### 多个部分
 
 - 多个值

```

// 打印，查询的权限

printer:print,query

```

- 所有的值

```

// 打印，查询的权限

printer:query,print,manage

printer:*

*:view

```

- 实例级别的控制


```

printer:query:lp7200
printer:print:epsoncolor

```

