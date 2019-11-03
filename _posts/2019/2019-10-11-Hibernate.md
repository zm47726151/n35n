## Hibernate

### 为什么要使用 hibernate？

对JDBC访问数据库的代码做了封装，大大简化了数据访问层繁琐的重复性代码。

Hibernate是一个基于JDBC的主流持久化框架，是一个优秀的ORM实现。他很大程度的简化DAO层的编码工作

hibernate使用Java反射机制，而不是字节码增强程序来实现透明性。

hibernate的性能非常好，因为它是个轻量级框架。映射的灵活性很出色。它支持各种关系数据库，从一对一到多对多的各种复杂关系。

### 什么是 ORM 框架？

对象-关系映射（Object-Relational Mapping，简称ORM），面向对象的开发方法是当今企业级应用开发环境中的主流开发方法，关系数据库是企业级应用环境中永久存放数据的主流数据存储系统。对象和关系数据是业务实体的两种表现形式，业务实体在内存中表现为对象，在数据库中表现为关系数据。内存中的对象之间存在关联和继承关系，而在数据库中，关系数据无法直接表达多对多关联和继承关系。因此，对象-关系映射(ORM)系统一般以中间件的形式存在，主要实现程序对象到关系数据库数据的映射.

### hibernate 中如何在控制台查看打印的 sql 语句？

### hibernate 有几种查询方式？

hql查询

sql查询

条件查询

```java

hql查询，sql查询，条件查询

HQL:  Hibernate Query Language. 面向对象的写法:
Query query = session.createQuery("from Customer where name = ?");
query.setParameter(0, "苍老师");
Query.list();



QBC:  Query By Criteria.(条件查询)
Criteria criteria = session.createCriteria(Customer.class);
criteria.add(Restrictions.eq("name", "花姐"));
List<Customer> list = criteria.list();



SQL:
SQLQuery query = session.createSQLQuery("select * from customer");
List<Object[]> list = query.list();

SQLQuery query = session.createSQLQuery("select * from customer");
query.addEntity(Customer.class);
List<Customer> list = query.list();



Hql： 具体分类
1、 属性查询 2、 参数查询、命名参数查询 3、 关联查询 4、 分页查询 5、 统计函数



HQL和SQL的区别

HQL是面向对象查询操作的，SQL是结构化查询语言 是面向数据库表结构的

```

### hibernate 实体类可以被定义为 final 吗？

可以将Hibernate的实体类定义为final类，但这种做法并不好。因为Hibernate会使用代理模式在延迟关联的情况下提高性能，如果你把实体类定义成final类之后，因为 Java不允许对final类进行扩展，所以Hibernate就无法再使用代理了，如此一来就限制了使用可以提升性能的手段。不过，如果你的持久化类实现了一个接口而且在该接口中声明了所有定义于实体类中的所有public的方法轮到话，你就能够避免出现前面所说的不利后果。

### 在 hibernate 中使用 Integer 和 int 做映射有什么区别？

在Hibernate中，如果将OID定义为Integer类型，那么Hibernate就可以根据其值是否为null而判断一个对象是否是临时的，如果将OID定义为了int类型，还需要在hbm映射文件中设置其unsaved-value属性为0。

### hibernate 是如何工作的？

hibernate工作原理：

![hibernate工作原理](http://qiniu.wsxxg.cn/20190403231419411.png)

### 说一下 hibernate 的缓存机制？

Hibernate中的缓存分为一级缓存和二级缓存。

一级缓存就是 Session 级别的缓存，在事务范围内有效是,内置的不能被卸载。二级缓存是 SesionFactory级别的缓存，从应用启动到应用结束有效。是可选的，默认没有二级缓存，需要手动开启。保存数据库后，缓存在内存中保存一份，如果更新了数据库就要同步更新。

什么样的数据适合存放到第二级缓存中？

- 很少被修改的数据，帖子的最后回复时间

- 经常被查询的数据，电商的地点

- 不是很重要的数据，允许出现偶尔并发的数据

- 不会被并发访问的是数据

- 常量数据

扩展：hibernate的二级缓存默认是不支持分布式缓存的。使用 memcahe,redis等中央缓存来代替二级缓存。

### hibernate 对象有哪些状态？

hibernate里对象有三种状态：

Transient（瞬时）：对象刚new出来，还没设id，设了其他值。

Persistent（持久）：调用了save()、saveOrUpdate()，就变成Persistent，有id。

etached（脱管）：当session close()完之后，变成Detached。

![hibernate工作原理](http://qiniu.wsxxg.cn/20190403231622847.png)

### 在 hibernate 中 getCurrentSession 和 openSession 的区别是什么？

openSession 从字面上可以看得出来，是打开一个新的session对象，而且每次使用都是打开一个新的session，假如连续使用多次，则获得的session不是同一个对象，并且使用完需要调用close方法关闭session。

getCurrentSession ，从字面上可以看得出来，是获取当前上下文一个session对象，当第一次使用此方法时，会自动产生一个session对象，并且连续使用多次时，得到的session都是同一个对象，这就是与openSession的区别之一，简单而言，getCurrentSession 就是：如果有已经使用的，用旧的，如果没有，建新的。

注意：在实际开发中，往往使用getCurrentSession多，因为一般是处理同一个事务（即是使用一个数据库的情况），所以在一般情况下比较少使用openSession或者说openSession是比较老旧的一套接口了。

### hibernate 实体类必须要有无参构造函数吗？为什么？

必须，因为hibernate框架会调用这个默认构造方法来构造实例对象，即Class类的newInstance方法，这个方法就是通过调用默认构造方法来创建实例对象的。

另外再提醒一点，如果你没有提供任何构造方法，虚拟机会自动提供默认构造方法（无参构造器），但是如果你提供了其他有参数的构造方法的话，虚拟机就不再为你提供默认构造方法，这时必须手动把无参构造器写在代码里，否则new Xxxx()是会报错的，所以默认的构造方法不是必须的，只在有多个构造方法时才是必须的，这里“必须”指的是“必须手动写出来”。

### hibernate如何操作数据库

首先呢先加载hibernate配置cfg.xml和解析hbm.xml映射文件还有初始化咱们的sessionFactory，然后由sessionFactory生产会话就是咱们的session，然后打开session，开启事务transaction，(不过咱们查询的时候是不需要开启事务的)执行相关增删改查（CRUD）后,提交或回滚事务，最后就是关闭资源。

### Hibernate五大核心（类/接口）简述

1 .Configuration接口的作用是对Hibernate进行配置，以及对它进行启动。（加载hibernate.cfg.xml）并创建一个SessionFactory对象。

2 .SessionFactory接口

- SessionFactory接口负责初始化Hibernate。它充当数据存储源的代理，并负责创建Session对象。SessionFactory是线程安全的。

3 .Session接口

- Session（会话）接口是Hibernate应用使用的主要接口。Session接口负责执行被持久化对象的CRUD操作(增删改查)。Session对象是非线程安全的。Session 相当于jdbc的connection

4 .Query与Criteria接口

- 总之Query和Criteria接口负责执行各种数据库查询。它可以使用HQL语句或SQL语句两种表达方式。

5 .Transaction接口

- Transaction（事务）接口是一个可选的API。负责操作相关的事务。

### Hibernate中的两大配置文件

*.hbm.xml：主键生成策略，映射关系，一对多，一对一的关系。

Hibernate.cfg.xml：方言(用哪个数据库)，数据库连接信息，包含*.hbm.xml内容，映射文件，也可以配事务。

### Hibernate事务处理

开启事务 session.beginTransaction();

执行相关的操作，如果成功则session.getTransaction().commit();

执行操作失败则 session.getTransaction.rollback();

### Hibernate的三种状态以及状态的转换
Transient(临时)

- new 一个初始化对象后，并没有在数据库里保存数据，处于临时状态；

Persistent(持久化)

- 当执行save()方法，调用session.close()方法之前，内存中的对象与数据库有           对应关系处于持久化状态；

Detached(脱管/游离)
- 当执行session.close()之后，处于脱管状态；

状态的转换

- 处于托管状态下，调用update()方法后，转换为持久化状态；

- 在持久化状态下，执行delete()方法后，转换为临时状态；

- 在未初始化对象之前，调用get(),load(),find(),iterate()之后，直接进入持久化	  状态。

###  Hibernate缓存

hibernate分为一级缓存即session缓存也叫事务级别的缓存以及查询缓存

二级缓存sessionFactory即应用级别的缓存,还有一个是查询缓存

一级缓存的生命周期和session的生命周期保持一致，

hibernate默认就启用了一级缓存，不能将其关闭，可以通过session.clear()和session.evict(object)来管理一级缓存。其中get,load,iterate都会使用一级缓存，一级缓存缓存的是对象。

二级缓存的生命周期和sessionFactory的生命周期保持一致，可以跨session,被多个session共享，hibernate3默认开启二级缓存,也可以手动开启并指定缓存插件如ehcache,oscache等。二级缓存也只能缓存对象。

查询缓存，查询缓存是针对普通属性结果集的缓存,对实体对象的结果集只缓存id。对query.list()起作用，query.iterate不起作用，也就是query.iterate不使用查询缓存

### 延迟加载

延迟加载机制是为了避免一些无谓的性能开销而提出来的，所谓延迟加载就是当在真正需要数据的时候，才真正执行数据加载操作。在Hibernate中提供了对实体对象的延迟加载以及对集合的延迟加载，另外在Hibernate3中还提供了对属性的延迟加载。

### Hibernate 中get 和 load的区别

加载方式：

- load为延迟加载(返回的是一个只有id属性的代理,只有使用该对象属性时,才发出sql语句)；

- get为立即加载(执行时,会立即向数据库发出sql语句)

返回结果：

- load检索不到记录时,会抛异常(ObjectNotFoundException)
- get检索不到记录时,会返回null

