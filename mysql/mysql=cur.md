# MySQL 存储过程--游标

```
CREATE DEFINER=`root`@`localhost` PROCEDURE `update_message`()
BEGIN
 declare v_teamId char(50);
 declare v_count int;
 DECLARE done int DEFAULT 0;

  DECLARE cur cursor for select userid from t_user ;
  -- 遍历数据结束标志
  
  -- 将结束标志绑定到游标
  DECLARE CONTINUE HANDLER FOR NOT FOUND SET done = 1; 
  
  open cur;
  set v_count = 0;
  read_loop : LOOP
	FETCH cur into v_teamId;

 if done != 0 then
	leave read_loop;
 end if;
 set v_count =v_count+1;
 update t_user_info set telephone=2 where userid =v_teamId ;
 end loop;	
 close cur;

END
```

