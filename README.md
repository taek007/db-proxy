# db-proxy

修改美团dbproxy源码

# 若SQL包含`关键字`, 词法分析会去掉`, 这里判断 token_id== TK_LITERAL,则加上`<br/>
2.增加批量insert功能<br/>
3.增加按字符串(hash)分表功能<br/>
4.增加按时间字段分表功能<br/>
5.id生成器, 自动填充分表主键id以及对应值, 主键id须为bigint  <br/>
6.修改后台管理show tables<br/>
```
mysql> show tables;
+---------+----------------+--------------+--------------+------------------------------------------------------------------+
| 库名    | 表名           | 分表字段     | 分表个数     | 分表字段类型 1:int, 2:string, 3:年, 4:年月, 5:年月日             |
+---------+----------------+--------------+--------------+------------------------------------------------------------------+
| ab   | xxx              | filepath     | 5            | 2                                                                |
| ab   | table_uid        | uid          | 4            | 1                                                                |
| ab   | user             | create_time  | 0            | 3                                                                |
+---------+----------------+--------------+--------------+------------------------------------------------------------------+
3 rows in set (0.00 sec)

select * from pwds;
mysql> select * from pwds;
+----------+----------+-------+----------+-------+-------------+------------+------------+-----------+
| username | password | hosts | backends | type  | master-user | master-pwd | slave-user | slave-pwd |
+----------+----------+-------+----------+-------+-------------+------------+------------+-----------+
| %        |          |       |          | proxy |             |            |            |           |
| test     | 7O7YJJEK |       |          | proxy | root        | 7O3aIZUN   | root       | 7O7YJJEK  |
| admin    | vLiGeco= |       |          | admin | NULL        | NULL       | NULL       | NULL      |
+----------+----------+-------+----------+-------+-------------+------------+------------+-----------+
3 rows in set (0.00 sec)
```
