# 什么是redis当中的事务？
Redis当中的事务与传统关系型数据库的事务是不同的， redis 的事务是一组命令的集合， 事务保证了集合当中命令执行完
不被其他的命令插入其中

redis的事务可以保证一个事务内的命令一次执行而不被其他命令插入影响。 