**MyBatis的执行流程如下：**
1. 读取MyBatis配置文件mybatis-config.xml。
2. 构造会话工厂SqlSessionFactory。
3. 会话工厂创建SqlSession对象。
4. 操作数据

<img width="679" alt="Image" src="https://github.com/user-attachments/assets/e2c0cb54-41cb-4c51-a02b-6f521f6ad0ea" />

库的接口，Executor执行器。
5. Executor执行方法中的MappedStatement参数。
6. 输入参数映射。
7. 输出结果映射。

**Mybatis是否支持延迟加载**
MyBatis支持延迟加载，即在需要用到数据时才加载。可以通过配置文件中的lazyLoadingEnabled配置启用或禁用延迟加载。

**延迟加载的底层原理**
延迟加载的底层原理主要使用CGLIB动态代理实现：
1. 使用CGLIB创建目标对象的代理对象。
2. 调用目标方法时，如果发现是null值，则执行SQL查询。
3. 获取数据后，设置属性值并继续查询目标方法。

**Mybatis的一级、二级缓存？**
MyBatis的一级缓存是基于PerpetualCache的HashMap本地缓存，作用域为Session，默认开启。二级缓存需要单独开启，作用域为Namespace或mapper，默认也是采用PerpetualCache，HashMap存储。

**Mybatis的二级缓存什么时候会清理缓存中的数据**
当作用域（一级缓存Session/二级缓存Namespaces）进行了新增、修改、删除操作后，默认该作用域下所有select中的缓存将被清空。
 
**两阶段锁协议（2PL）**
保证可串行化调度的一种并发控制协议是两阶段锁协议，该协议不需要提前知道事务的所有操作，协议要求事务分两个阶段提出加锁和解锁请求。 增长阶段：事务从 LockManager 处获取锁，不能释放任何锁。 缩减阶段：事务只能释放锁或降级锁，不能获取任何新锁

**WAL（预写日志）机制**
是一种用于数据库系统的日志记录技术，其核心思想是在对数据库进行任何持久性更改之前，先将更改记录到一个日志文件中。这样做的目的是为了确保事务的持久性和一致性，即使在系统崩溃或意外关闭的情况下，未完成的事务数据也不会丢失。WAL机制的实现通常包括以下步骤：记录日志、执行更改、以及在适当的时候将更改应用到数据库中。在MySQL等数据库中，WAL机制可以有效降低随机写入的性能消耗，并确保数据的安全性。