# 分布式事务
## 理论
> CAP  
>* 一致性 Consistency
>* 可用性 Availability
>* 分区容错性 Partition torebalance  
一个分布式系统不可能同时满足这3个条件，最多只能满足其中两项，要么 AP，要么 CP，要么 AC，但是不存在 CAP  
>>*如Eureka满足AP*

> BASE
>* 基本可用 Basic Available
>* 软状态 Soft State
>* 最终一致性 Eventually Consistency   
BASE 理论是对 Cap 中的一致性和可用性权衡的结果，其来源于大规模分布式系统实践的总结，是基于 Cap 逐步演化而来，其核心思想是即使无法做到强一致性，但每个应用都可以根据自身的业务特点，采用适当的方法是使用达到最终一致性

## 2PC
## 3PC
## TCC