# MyBatis核心组件
>
## 持久层的概念和MyBatis的特点
>
- 持久层可以将业务数据存储到磁盘，具备长期存储能力，一般执行持久任务的都是数据库系统。
>
### MyBatis的特点
>
- 1 不屏蔽SQL
- 2 提供强大、灵活的映射机制
- 3 MyBatis提供了使用Mapper的接口编程
>
## MyBatis的核心组件
>
- **SqlSessionFactoryBuilder**(构造器)：根据配置或者代码来生成SqlSessionFactory，使用的是分步构建的Builder模式
>
- **SqlSessionFactory**(工厂接口)：依靠它来生成SqlSession，使用的是工厂模式。
>
- **SqlSession**(会话)：既可以发送SQL执行返回结果，也可以获取Mapper的接口。
>
- **SQL Mapper**(映射器)：由一个Java接口和XML文件(或者注解)构成，需要给出对应的SQL和映射规则。
>
## SqlSessionFactory
>
- 使用MyBatis首先是使用配置或者代码去生产SqlSessionFactory，MyBatis提供了构造器SqlSessionFactoryBuilder。
- 既可以通过读取配置的XML文件的形式生成SqlSessionFactory，也可以通过Java代码的形式去生成SqlSessionFactory。
>
## SqlSession
>
- MyBatis中，SqlSession是其核心接口。由两个实现类：DefaultSqlSession(单线程)，SqlSessionManager(多线程)。SqlSession的作用类似于一个JDBC中的Connection对象，代表着一个连接资源的启用。
- 具体作用有3个：获取Mapper接口、发送SQL给数据库、控制数据库事务。
- 创建SqlSession：`SqlSession sqlSession = sqlSessionFactory.openSession();`
>
## 映射器
>
- 映射器是MyBatis中最重要、最复杂的组件，它由一个接口和对应的XML文件(或注解)组成。可以配置以下内容
>
- 描述映射规则
- 提供SQL语句，配置SQL参数类型、返回类型、缓存刷新等信息
- 配置缓存
- 提供动态SQL
>
## 生命周期
>
- 生命周期是组件的重要问题，尤其是在多线程的环境中。生命周期就是每一个对象应该存活的时间。
>
### SqlSessionFactoryBuilder
- 只存在于创建SqlSessionFactory的方法中。
>
### SqlSessionFactory
- SqlSessionFactory可以被认为是一个数据库连接池，生命周期存在于整个MyBatis的应用之中。
>
### SqlSession
- SqlSession相当于一个数据库连接(Connection对象)，存活在一个业务请求中，处理完整个请求后，应该关闭这条连接，归还给SqlSessionFactory。
>
### Mapper
- 由SqlSession创建，生命周期小于等于SqlSession的生命周期。
>
## 实例
>
-