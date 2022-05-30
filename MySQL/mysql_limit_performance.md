# 分页查询性能

假设有数据表 **t_account** ,结构如下：  
```sql
create t_account(
    id bigint(20) unsigned not null auto_increment comment '主键',
    account_no varchar(64) not null default '' comment '账户编码',
    account_name varchar(200) not null default '' comment '账户名称',
    account_type varchar(4) not null default '' comment '账户类型',
    status char(1) not null default '' comment '账户状态',
    balance decimal(19,4) not null default 0 comment '余额',
    gmt_created timestamp not null default current_timestamp comment '创建时间',
    gmt_modified timestamp not null default current_timestamp on update current_timestamp comment '修改时间',
    primary key (`id`),
    unique key `uk_account` (`account_no`),
    index `idx_status` (`status`),
    index `idx_gmt_created` (`gmt_created`)
) default character set=utf8mb4 comment='账户';
```
MySQL分页查询预发如下
```select * from table limit offset,row;```  

假设账户表 **t_account** 有2000w条数据，对下进行分页查询结果如下:  
```sql
select * from t_account limit 1, 10  // 32.8ms
select * from t_account limit 10, 10 // 34.2ms
select * from t_account limit 100, 10 // 35.4ms
select * from t_account limit 1000, 10 // 39.6ms
select * from t_account limit 10000, 10 // 5660ms
select * from t_account limit 100000, 10 // 61.4 秒
select * from t_account limit 1000000, 10 // 273 秒
```  
可以看到，随着偏移量（offset）的增加，查询时间变得越长。对于普通的业务而言，超过1秒的查询是绝对不可以忍受的。

以上数据，我们可以总结出：**LIMIT** 分页查询的时间与偏移量值成正比。当偏移量越大时，查询时间越长。这种情况，会随着业务的增加，数据的增多，会越发的明显。那么，如何优化这种情况呢？  
答案是：**覆盖索引**

## 优化方式
### 子查询方式
```sql
select * 
from t_account
where id >= (select id from t_account limit 100000,1)
limit 20; // 54ms
```
此种方式，首先通过 **子查询** 和 **覆盖索引** 定位到起始位置 **ID** ，然后再取所需条数的数据

### join查询方式
```sql
select *
from t_account ac
join (select id from t_account where status='N' limit 100000,10) ss
on ac.id = ss.id; //53.6 ms
```
这条SQL的含义是，通过自连接与join定位到目标的主键集合 (**ids**)，然后将数据取出。  
在定位目标 **ids** 时，由于 SELECT 的元素只有主键 ID，且status 存在索引，因此 **ss** 只需在索引中就能定位到目标 **ids**，不用在数据文件上进行查找。因而，查询效率非常高