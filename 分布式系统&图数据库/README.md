## 零、简介

> 在计算机科学中，图数据库（英语：graph database，GDB）是一个使用图结构进行语义查询的数据库，它使用节点、边和属性来表示和存储数据。该系统的关键概念是图，它直接将存储中的数据项，与数据节点和节点间表示关系的边的集合相关联。这些关系允许直接将存储区中的数据链接在一起，并且在许多情况下，可以通过一个操作进行检索。图数据库将数据之间的关系作为优先级。查询图数据库中的关系很快，因为它们永久存储在数据库本身中。可以使用图数据库直观地显示关系，使其对于高度互连的数据非常有用。
>
> 图数据库是一种非关系型数据库，以解决现有关系数据库的局限性。图模型明确地列出了数据节点之间的依赖关系，而关系模型和其他NoSQL数据库模型则通过隐式连接来链接数据。图数据库从设计上，就是可以简单快速地检索难以在关系系统中建模的复杂层次结构的。图数据库与20世纪70年代的网络模型数据库相似，它们都表示一般的图，但是网络模型数据库在较低的抽象层次上运行，并且不能轻松遍历一系列边。
>
> [维基百科](https://zh.wikipedia.org/zh-cn/%E5%9B%BE%E6%95%B0%E6%8D%AE%E5%BA%93)

## 一、NoSQL

1. #### 简介

   NoSQL（Not only SQL），是对不同于传统的关系数据库的数据库管理系统的统称。

2. #### 优点

   - 高扩展性
   - 分布式计算
   - 低成本
   - 架构的灵活性，半结构化数据
   - 没有复杂的关系

3. #### 缺点

   - 没有标准化
   - 有限的查询功能
   - 最终一致是不直观的程序

4. #### 分类

   |     类型      | 部分代表                             | 特点                                                         |
   | :-----------: | :----------------------------------- | ------------------------------------------------------------ |
   |    列存储     | Hbase<br />Cassandra<br />Hypertable | 列存储数据，方便存储结构化和半结构化数据，方便做数据压缩，对针对某一列或者某几列的查询有非常大的IO优势。 |
   |   文档存储    | MongoDB                              | 用类似json的格式存储，存储的内容是文档型的。有机会对某些字段建立索引，实现关系数据库的某些功能。 |
   | key-value存储 | Redis                                | 可以通过key快速查询到其value                                 |
   |    图存储     | Neo4J<br />FlockDB                   | 图形关系的最佳存储                                           |
   |   对象存储    | db4o<br />Versant                    | 通过类似面向对象语言的语法操作数据库，通过对象的方式存取数据。 |
   |   xml数据库   |                                      | 高效的存储XML数据，并支持XML的内部查询语法                   |

## 二、MongoDB

1. #### 简介

   MongoDB 是由**C++**语言编写的，是一个基于**分布式文件存储**的开源数据库系统。

   在高负载的情况下，添加更多的节点，可以保证服务器性能。

   MongoDB 旨在为**WEB应用**提供可扩展的高性能数据存储解决方案。

   MongoDB 将数据存储为一个**文档**，数据结构由键值(key=>value)对组成。MongoDB 文档类似于 JSON 对象。字段值可以包含其他文档，数组及文档数组。

   ![image-20210409170417133](..\images\image-20210409170417133.png)

2. #### 主要特点

   - 面向文档存储的数据库。
   - 如果负载的增加（需要更多的存储空间和更强的处理能力） ，它可以分布在计算机网络中的其他节点上这就是所谓的分片。
   - 支持丰富的查询表达式，查询指令使用JSON形式的标记，可轻易查询文档中内嵌的对象及数组。
   - 允许在服务端执行脚本，可以用Javascript编写某个函数，直接在服务端执行，也可以把函数的定义存储在服务端，下次直接调用即可。
   - 支持各种编程语言:RUBY，PYTHON，JAVA，C++，PHP，C#等多种语言。
   - 安装简单。

## 三、Redis

1. #### 简介

   Redis是一个使用ANSI C编写的开源、支持网络、基于内存、分布式、可选持久性的**键值对存储**数据库。

2. #### 特点

   - 支持数据的持久化，可以将内存中的数据保存在磁盘中，重启的时候可以再次加载进行使用。
   - 不仅仅支持简单的key-value类型的数据，同时还提供list，set，zset，hash等数据结构的存储。
   - 支持数据的备份，即master-slave模式的数据备份。

3. #### 优势

   - 性能极高。
   - 丰富的数据类型 – Redis支持二进制案例的 Strings, Lists, Hashes, Sets 及 Ordered Sets 数据类型操作。
   - 原子 – Redis的所有操作都是原子性的，意思就是要么成功执行要么失败完全不执行。单个操作是原子性的。多个操作也支持事务，即原子性，通过MULTI和EXEC指令包起来。
   - 丰富的特性 – Redis还支持 publish/subscribe, 通知, key 过期等等特性。

## 四、分布式系统

1. 简介

   分布式系统是由一组通过网络进行通信、为了完成共同的任务而协调工作的计算机节点组成的系统。

   分布式系统的出现是为了用廉价的、普通的机器完成单个计算机无法完成的计算、存储任务。

   其目的是**利用更多的机器，处理更多的数据**。

2. partition与replication

   分布式系统通过分片（**partition**，分而治之）将任务分发到这些计算机节点。对于计算，那么就是对计算任务进行切换，每个节点算一些，最终汇总就行了，这就是MapReduce的思想；对于存储，更好理解一下，每个节点存一部分数据就行了。当数据规模变大的时候，Partition是唯一的选择，同时也会带来一些好处：

   　　（1）提升性能和并发，操作被分发到不同的分片，相互独立

   　　（2）提升系统的可用性，即使部分分片不能用，其他分片不会受到影响

   理想的情况下，有分片就行了，但事实的情况却不大理想。原因在于，分布式系统中有大量的节点，且通过网络通信。单个节点的故障（进程crash、断电、磁盘损坏）是个小概率事件，但整个系统的故障率会随节点的增加而指数级增加，网络通信也可能出现断网、高延迟的情况。在这种一定会出现的“异常”情况下，分布式系统还是需要继续稳定的对外提供服务，即需要较强的容错性。最简单的办法，就是冗余或者复制集（**Replication**），即多个节点负责同一个任务，最为常见的就是分布式存储中，多个节点复杂存储同一份数据，以此增强可用性与可靠性。同时，Replication也会带来性能的提升，比如数据的locality可以减少用户的等待时间。

   ![replication&partition](..\images\replication&partition.png)

3. 挑战

   - 异构的机器与网络

     分布式系统中的机器，配置不一样，其上运行的服务也可能由不同的语言、架构实现，因此处理能力也不一样；节点间通过网络连接，而不同网络运营商提供的网络的带宽、延时、丢包率又不一样。怎么保证大家齐头并进，共同完成目标，这四个不小的挑战。

   - 普遍的节点故障

     虽然单个节点的故障概率较低，但节点数目达到一定规模，出故障的概率就变高了。分布式系统需要保证故障发生的时候，系统仍然是可用的，这就需要监控节点的状态，在节点故障的情况下将该节点负责的计算、存储任务转移到其他节点。

   - 不可靠的网络

     节点间通过网络通信，而网络是不可靠的。可能的网络问题包括：网络分割、延时、丢包、乱序

   总而言之，分布式的挑战来自**不确定性**，不确定计算机什么时候crash、断电，不确定磁盘什么时候损坏，不确定每次网络通信要延迟多久，也不确定通信对端是否处理了发送的消息。而分布式的规模放大了这个不确定性，不确定性是令人讨厌的，所以有诸多的分布式理论、协议来保证在这种不确定性的情况下，系统还能继续正常工作。

4. 特征与衡量标准

   - 透明性

     使用分布式系统的用户并不关心系统是怎么实现的，也不关心读到的数据来自哪个节点，对用户而言，分布式系统的最高境界是用户根本感知不到这是一个分布式系统

   - 可扩展性

     分布式系统的根本目标就是为了处理单个计算机无法处理的任务，当任务增加的时候，分布式系统的处理能力需要随之增加。简单来说，要比较方便的通过增加机器来应对数据量的增长，同时，当任务规模缩减的时候，可以撤掉一些多余的机器，达到动态伸缩的效果

   - 可用性与可靠性

     一般来说，分布式系统是需要长时间甚至7*24小时提供服务的。可用性是指系统在各种情况对外提供服务的能力，简单来说，可以通过不可用时间与正常服务时间的必知来衡量；而可靠性而是指计算结果正确、存储的数据不丢失。

   - 高性能

     不管是单机还是分布式系统，大家都非常关注性能。不同的系统对性能的衡量指标是不同的，最常见的：高并发，单位时间内处理的任务越多越好；低延迟：每个任务的平均时间越少越好。这个其实跟操作系统CPU的调度策略很像

   - 一致性

     分布式系统为了提高可用性可靠性，一般会引入冗余（复制集）。那么如何保证这些节点上的状态一致，这就是分布式系统不得不面对的一致性问题。一致性有很多等级，一致性越强，对用户越友好，但会制约系统的可用性；一致性等级越低，用户就需要兼容数据不一致的情况，但系统的可用性、并发性很高很多。

5. 过程与架构

   用户使用web、app等通过tcp、http连接到系统，在分布式系统中，使用负载均衡（load balance）找到一个节点，处理请求。请求有可能简单，也有可能很复杂。简单的请求，比如读取数据，那么很可能是有缓存的，即分布式缓存，如果缓存没有命中，那么需要去数据库拉取数据。对于复杂的请求，可能会调用到系统中其他的服务。

   假设服务A需要调用服务B的服务，首先两个节点需要通信，网络通信都是建立在TCP/IP协议的基础上，但是，每个应用都手写socket是一件冗杂、低效的事情，因此需要应用层的封装，因此有了HTTP、FTP等各种应用层协议。当系统愈加复杂，提供大量的http接口也是一件困难的事情。因此，有了更进一步的抽象，那就是RPC（remote produce call），是的远程调用就跟本地过程调用一样方便，屏蔽了网络通信等诸多细节，增加新的接口也更加方便。

   一个请求可能包含诸多操作，即在服务A上做一些操作，然后在服务B上做另一些操作。比如简化版的网络购物，在订单服务上发货，在账户服务上扣款。这两个操作需要保证原子性，要么都成功，要么都不操作。这就涉及到分布式事务的问题，分布式事务是从应用层面保证一致性：某种守恒关系。

   上面说道一个请求包含多个操作，其实就是涉及到多个服务，分布式系统中有大量的服务，每个服务又是多个节点组成。那么一个服务怎么找到另一个服务（的某个节点呢）？通信是需要地址的，怎么获取这个地址，最简单的办法就是配置文件写死，或者写入到数据库，但这些方法在节点数据巨大、节点动态增删的时候都不大方便，这个时候就需要服务注册与发现：提供服务的节点向一个协调中心注册自己的地址，使用服务的节点去协调中心拉取地址。

   从上可以看见，协调中心提供了中心化的服务：以一组节点提供类似单点的服务，使用非常广泛，比如命令服务、分布式锁。协调中心最出名的就是chubby，zookeeper。

   回到用户请求这个点，请求操作会产生一些数据、日志，通常为信息，其他一些系统可能会对这些消息感兴趣，比如个性化推荐、监控等，这里就抽象出了两个概念，消息的生产者与消费者。那么生产者怎么讲消息发送给消费者呢，RPC并不是一个很好的选择，因为RPC肯定得指定消息发给谁，但实际的情况是生产者并不清楚、也不关心谁会消费这个消息，这个时候消息队列就出马了。简单来说，生产者只用往消息队列里面发就行了，队列会将消息按主题（topic）分发给关注这个主题的消费者。消息队列起到了异步处理、应用解耦的作用。

   上面提到，用户操作会产生一些数据，这些数据忠实记录了用户的操作习惯、喜好，是各行各业最宝贵的财富。比如各种推荐、广告投放、自动识别。这就催生了分布式计算平台，比如Hadoop，Storm等，用来处理这些海量的数据。

   最后，用户的操作完成之后，用户的数据需要持久化，但数据量很大，大到按个节点无法存储，那么这个时候就需要分布式存储：将数据进行划分放在不同的节点上，同时，为了防止数据的丢失，每一份数据会保存多分。传统的关系型数据库是单点存储，为了在应用层透明的情况下分库分表，会引用额外的代理层。而对于NoSql，一般天然支持分布式。

   ![分布式架构](..\images\分布式.png)

6. 概念

   - 负载均衡：

   　　　　Nginx：高性能、高并发的web服务器；功能包括负载均衡、反向代理、静态内容缓存、访问控制；工作在应用层

   　　　　LVS： Linux virtual server，基于集群技术和Linux操作系统实现一个高性能、高可用的服务器；工作在网络层

   - webserver：

   　　　　Java：Tomcat，Apache，Jboss

   　　　　Python：gunicorn、uwsgi、twisted、webpy、tornado

   - service：　　

   　　　　SOA、微服务、spring boot，django

   - 容器：

   　　　　docker，kubernetes

   - cache：

   　　　　memcache、redis等

   - 协调中心：

   　　　　zookeeper、etcd等

   　　　　zookeeper使用了Paxos协议Paxos是强一致性，高可用的去中心化分布式。zookeeper的使用场景非常广泛，之后细讲。

   - rpc框架：

   　　　　grpc、dubbo、brpc

   　　　　dubbo是阿里开源的Java语言开发的高性能RPC框架，在阿里系的诸多架构中，都使用了dubbo + spring boot

   - 消息队列：

   　　　　kafka、rabbitMQ、rocketMQ、QSP

   　　　　消息队列的应用场景：异步处理、应用解耦、流量削锋和消息通讯

   - 实时数据平台：

   　　　　storm、akka

   - 离线数据平台：

   　　　　hadoop、spark

   　　　　PS: apark、akka、kafka都是scala语言写的，看到这个语言还是很牛逼的

   - dbproxy：

   　　　　cobar也是阿里开源的，在阿里系中使用也非常广泛，是关系型数据库的sharding + replica 代理

   - db：

   　　　　mysql、oracle、MongoDB、HBase

   - 搜索：

   　　　　elasticsearch、solr

   - 日志：

   　　　　rsyslog、elk、flume