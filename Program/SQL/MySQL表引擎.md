# MySQL表引擎

**区别于其他数据库的最重要的特点就是其插件式的表存储引擎。切记：存储引擎是基于表的，而不是数据库。**

MyISAM、InnoDB、BDB（BerkeleyDB）、Merge、Memory（Heap）、Example、Federated、
Archive、CSV、Blackhole、MaxDB 等等十几个引擎

## InnoDB与MyISAM的区别：
### InnoDB存储引擎: 主要面向OLTP(Online Transaction Processing，在线事务处理)方面的应用，是第一个完整支持ACID事务的存储引擎(BDB第一个支持事务的存储引擎，已经停止开发)。

#### 特点：
- 行锁设计、支持外键；
- 支持类似于Oracle风格的一致性非锁定读(即：默认情况下读取操作不会产生锁)；
- InnoDB将数据放在一个逻辑的表空间中，由InnoDB自身进行管理。从MySQL4.1版本开始，可以将每个InnoDB存储引擎的表单独存放到一个独立的ibd文件中；
- InnoDB通过使用MVCC(多版本并发控制：读不会阻塞写，写也不会阻塞读)来获得高并发性，并且实现了SQL标准的4种隔离级别(默认为REPEATABLE级别)；
- InnoDB还提供了插入缓冲(insert buffer)、二次写(double write)、自适应哈希索引(adaptive hash index)、预读(read ahead)等高性能和高可用的功能；
- InnoDB采用了聚集(clustered)的方式来存储表中的数据，每张标的存储都按主键的顺序存放(如果没有显式的在建表时指定主键，InnoDB会为每一行生成一个6字节的ROWID，并以此作为主键)；
- InnoDB表会有三个隐藏字段：除了上面提到了6字节的DB_ROW_ID外，还有6字节的DB_TX_ID(事务ID)和7字节的DB_ROLL_PTR(指向对应回滚段的地址)。这个可以通过innodb monitor看到；

### MyISAM存储引擎: 是MySQL官方提供的存储引擎，主要面向OLAP(Online Analytical Processing,在线分析处理)方面的应用。
#### 特点：
- 不支持事务，支持表所和全文索引。操作速度快；
- MyISAM存储引擎表由MYD和MYI组成，MYD用来存放数据文件，MYI用来存放索引文件。MySQL数据库只缓存其索引文件，数据文件的缓存交给操作系统本身来完成；
- MySQL5.0版本开始，MyISAM默认支持256T的单表数据；

