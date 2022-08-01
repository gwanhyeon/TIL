# trouble shooting-2

- trouble :
    
    

```jsx
org.h2.jdbc.JdbcSQLNonTransientConnectionException: A file path that is implicitly relative to the current working directory is not allowed in the database URL "jdbc:h2:membership:test". Use an absolute path, ~/name, ./name, or the baseDir setting instead. [90011-214]
    at org.h2.message.DbException.getJdbcSQLException(DbException.java:678) ~[h2-2.1.214.jar:2.1.214]
    at org.h2.message.DbException.getJdbcSQLException(DbException.java:477) ~[h2-2.1.214.jar:2.1.214]
    at org.h2.message.DbException.get(DbException.java:223) ~[h2-2.1.214.jar:2.1.214]
    at org.h2.message.DbException.get(DbException.java:199) ~[h2-2.1.214.jar:2.1.214]
    at org.h2.engine.ConnectionInfo.getName(ConnectionInfo.java:464) ~[h2-2.1.214.jar:2.1.214]
    at org.h2.engine.Engine.openSession(Engine.java:49) ~[h2-2.1.214.jar:2.1.214]
    at org.h2.engine.Engine.openSession(Engine.java:222) ~[h2-2.1.214.jar:2.1.214]
    at org.h2.engine.Engine.createSession(Engine.java:201) ~[h2-2.1.214.jar:2.1.214]
    at org.h2.engine.SessionRemote.connectEmbeddedOrServer(SessionRemote.java:338) ~[h2-2.1.214.jar:2.1.214]
    at org.h2.jdbc.JdbcConnection.<init>(JdbcConnection.java:122) ~[h2-2.1.214.jar:2.1.214]
    at org.h2.Driver.connect(Driver.java:59) ~[h2-2.1.214.jar:2.1.214]
    at com.zaxxer.hikari.util.DriverDataSource.getConnection(DriverDataSource.java:138) ~[HikariCP-4.0.3.jar:na]
    at com.zaxxer.hikari.pool.PoolBase.newConnection(PoolBase.java:364) ~[HikariCP-4.0.3.jar:na]
    at com.zaxxer.hikari.pool.PoolBase.newPoolEntry(PoolBase.java:206) ~[HikariCP-4.0.3.jar:na]
    at com.zaxxer.hikari.pool.HikariPool.createPoolEntry(HikariPool.java:476) ~[HikariCP-4.0.3.jar:na]
    at com.zaxxer.hikari.pool.HikariPool.checkFailFast(HikariPool.java:561) ~[HikariCP-4.0.3.jar:na]
    at com.zaxxer.hikari.pool.HikariPool.<init>(HikariPool.java:115) ~[HikariCP-4.0.3.jar:na]
    at com.zaxxer.hikari.HikariDataSource.getConnection(HikariDataSource.java:112) ~[HikariCP-4.0.3.jar:na]
    at org.hibernate.engine.jdbc.connections.internal.DatasourceConnectionProviderImpl.getConnection(DatasourceConnectionProviderImpl.java:122) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
    at org.hibernate.engine.jdbc.env.internal.JdbcEnvironmentInitiator$ConnectionProviderJdbcConnectionAccess.obtainConnection(JdbcEnvironmentInitiator.java:181) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
    at org.hibernate.engine.jdbc.env.internal.JdbcEnvironmentInitiator.initiateService(JdbcEnvironmentInitiator.java:68) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
    at org.hibernate.engine.jdbc.env.internal.JdbcEnvironmentInitiator.initiateService(JdbcEnvironmentInitiator.java:35) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
    at org.hibernate.boot.registry.internal.StandardServiceRegistryImpl.initiateService(StandardServiceRegistryImpl.java:101) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
    at org.hibernate.service.internal.AbstractServiceRegistryImpl.createService(AbstractServiceRegistryImpl.java:263) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
    at org.hibernate.service.internal.AbstractServiceRegistryImpl.initializeService(AbstractServiceRegistryImpl.java:237) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
    at org.hibernate.service.internal.AbstractServiceRegistryImpl.getService(AbstractServiceRegistryImpl.java:214) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
    at org.hibernate.id.factory.internal.DefaultIdentifierGeneratorFactory.injectServices(DefaultIdentifierGeneratorFactory.java:175) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
    at org.hibernate.service.internal.AbstractServiceRegistryImpl.injectDependencies(AbstractServiceRegistryImpl.java:286) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
    at org.hibernate.service.internal.AbstractServiceRegistryImpl.initializeService(AbstractServiceRegistryImpl.java:243) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
    at org.hibernate.service.internal.AbstractServiceRegistryImpl.getService(AbstractServiceRegistryImpl.java:214) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
    at org.hibernate.boot.internal.InFlightMetadataCollectorImpl.<init>(InFlightMetadataCollectorImpl.java:173) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
    at org.hibernate.boot.model.process.spi.MetadataBuildingProcess.complete(MetadataBuildingProcess.java:127) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
    at org.hibernate.jpa.boot.internal.EntityManagerFactoryBuilderImpl.metadata(EntityManagerFactoryBuilderImpl.java:1460) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
    at org.hibernate.jpa.boot.internal.EntityManagerFactoryBuilderImpl.build(EntityManagerFactoryBuilderImpl.java:1494) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
    at org.springframework.orm.jpa.vendor.SpringHibernateJpaPersistenceProvider.createContainerEntityManagerFactory(SpringHibernateJpaPersistenceProvider.java:58) ~[spring-orm-5.3.22.jar:5.3.22]
    at org.springframework.orm.jpa.LocalContainerEntityManagerFactoryBean.createNativeEntityManagerFactory(LocalContainerEntityManagerFactoryBean.java:365) ~[spring-orm-5.3.22.jar:5.3.22]
    at org.springframework.orm.jpa.AbstractEntityManagerFactoryBean.buildNativeEntityManagerFactory(AbstractEntityManagerFactoryBean.java:409) ~[spring-orm-5.3.22.jar:5.3.22]
    at org.springframework.orm.jpa.AbstractEntityManagerFactoryBean.afterPropertiesSet(AbstractEntityManagerFactoryBean.java:396) ~[spring-orm-5.3.22.jar:5.3.22]
    at org.springframework.orm.jpa.LocalContainerEntityManagerFactoryBean.afterPropertiesSet(LocalContainerEntityManagerFactoryBean.java:341) ~[spring-orm-5.3.22.jar:5.3.22]
    at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.invokeInitMethods(AbstractAutowireCapableBeanFactory.java:1863) ~[spring-beans-5.3.22.jar:5.3.22]
    at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.initializeBean(AbstractAutowireCapableBeanFactory.java:1800) ~[spring-beans-5.3.22.jar:5.3.22]
    at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.doCreateBean(AbstractAutowireCapableBeanFactory.java:620) ~[spring-beans-5.3.22.jar:5.3.22]
    at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.createBean(AbstractAutowireCapableBeanFactory.java:542) ~[spring-beans-5.3.22.jar:5.3.22]
    at org.springframework.beans.factory.support.AbstractBeanFactory.lambda$doGetBean$0(AbstractBeanFactory.java:335) ~[spring-beans-5.3.22.jar:5.3.22]
    at org.springframework.beans.factory.support.DefaultSingletonBeanRegistry.getSingleton(DefaultSingletonBeanRegistry.java:234) ~[spring-beans-5.3.22.jar:5.3.22]
    at org.springframework.beans.factory.support.AbstractBeanFactory.doGetBean(AbstractBeanFactory.java:333) ~[spring-beans-5.3.22.jar:5.3.22]
    at org.springframework.beans.factory.support.AbstractBeanFactory.getBean(AbstractBeanFactory.java:208) ~[spring-beans-5.3.22.jar:5.3.22]
    at org.springframework.context.support.AbstractApplicationContext.getBean(AbstractApplicationContext.java:1154) ~[spring-context-5.3.22.jar:5.3.22]
    at org.springframework.context.support.AbstractApplicationContext.finishBeanFactoryInitialization(AbstractApplicationContext.java:908) ~[spring-context-5.3.22.jar:5.3.22]
    at org.springframework.context.support.AbstractApplicationContext.refresh(AbstractApplicationContext.java:583) ~[spring-context-5.3.22.jar:5.3.22]
    at org.springframework.boot.web.servlet.context.ServletWebServerApplicationContext.refresh(ServletWebServerApplicationContext.java:147) ~[spring-boot-2.7.2.jar:2.7.2]
    at org.springframework.boot.SpringApplication.refresh(SpringApplication.java:734) ~[spring-boot-2.7.2.jar:2.7.2]
    at org.springframework.boot.SpringApplication.refreshContext(SpringApplication.java:408) ~[spring-boot-2.7.2.jar:2.7.2]
    at org.springframework.boot.SpringApplication.run(SpringApplication.java:308) ~[spring-boot-2.7.2.jar:2.7.2]
    at org.springframework.boot.SpringApplication.run(SpringApplication.java:1306) ~[spring-boot-2.7.2.jar:2.7.2]
    at org.springframework.boot.SpringApplication.run(SpringApplication.java:1295) ~[spring-boot-2.7.2.jar:2.7.2]
    at com.kgh.membership.MembershipApplication.main(MembershipApplication.java:10) ~[main/:na]

2022-08-02 01:02:07.310  WARN 30126 --- [           main] o.h.e.j.e.i.JdbcEnvironmentInitiator     : HHH000342: Could not obtain connection to query metadata

org.h2.jdbc.JdbcSQLNonTransientConnectionException: A file path that is implicitly relative to the current working directory is not allowed in the database URL "jdbc:h2:membership:test". Use an absolute path, ~/name, ./name, or the baseDir setting instead. [90011-214]
    at org.h2.message.DbException.getJdbcSQLException(DbException.java:678) ~[h2-2.1.214.jar:2.1.214]
    at org.h2.message.DbException.getJdbcSQLException(DbException.java:477) ~[h2-2.1.214.jar:2.1.214]
    at org.h2.message.DbException.get(DbException.java:223) ~[h2-2.1.214.jar:2.1.214]
    at org.h2.message.DbException.get(DbException.java:199) ~[h2-2.1.214.jar:2.1.214]
    at org.h2.engine.ConnectionInfo.getName(ConnectionInfo.java:464) ~[h2-2.1.214.jar:2.1.214]
    at org.h2.engine.Engine.openSession(Engine.java:49) ~[h2-2.1.214.jar:2.1.214]
    at org.h2.engine.Engine.openSession(Engine.java:222) ~[h2-2.1.214.jar:2.1.214]
    at org.h2.engine.Engine.createSession(Engine.java:201) ~[h2-2.1.214.jar:2.1.214]
    at org.h2.engine.SessionRemote.connectEmbeddedOrServer(SessionRemote.java:338) ~[h2-2.1.214.jar:2.1.214]
    at org.h2.jdbc.JdbcConnection.<init>(JdbcConnection.java:122) ~[h2-2.1.214.jar:2.1.214]
    at org.h2.Driver.connect(Driver.java:59) ~[h2-2.1.214.jar:2.1.214]
    at com.zaxxer.hikari.util.DriverDataSource.getConnection(DriverDataSource.java:138) ~[HikariCP-4.0.3.jar:na]
    at com.zaxxer.hikari.pool.PoolBase.newConnection(PoolBase.java:364) ~[HikariCP-4.0.3.jar:na]
    at com.zaxxer.hikari.pool.PoolBase.newPoolEntry(PoolBase.java:206) ~[HikariCP-4.0.3.jar:na]
    at com.zaxxer.hikari.pool.HikariPool.createPoolEntry(HikariPool.java:476) ~[HikariCP-4.0.3.jar:na]
    at com.zaxxer.hikari.pool.HikariPool.checkFailFast(HikariPool.java:561) ~[HikariCP-4.0.3.jar:na]
    at com.zaxxer.hikari.pool.HikariPool.<init>(HikariPool.java:115) ~[HikariCP-4.0.3.jar:na]
    at com.zaxxer.hikari.HikariDataSource.getConnection(HikariDataSource.java:112) ~[HikariCP-4.0.3.jar:na]
    at org.hibernate.engine.jdbc.connections.internal.DatasourceConnectionProviderImpl.getConnection(DatasourceConnectionProviderImpl.java:122) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
    at org.hibernate.engine.jdbc.env.internal.JdbcEnvironmentInitiator$ConnectionProviderJdbcConnectionAccess.obtainConnection(JdbcEnvironmentInitiator.java:181) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
    at org.hibernate.engine.jdbc.env.internal.JdbcEnvironmentInitiator.initiateService(JdbcEnvironmentInitiator.java:68) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
    at org.hibernate.engine.jdbc.env.internal.JdbcEnvironmentInitiator.initiateService(JdbcEnvironmentInitiator.java:35) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
    at org.hibernate.boot.registry.internal.StandardServiceRegistryImpl.initiateService(StandardServiceRegistryImpl.java:101) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
    at org.hibernate.service.internal.AbstractServiceRegistryImpl.createService(AbstractServiceRegistryImpl.java:263) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
    at org.hibernate.service.internal.AbstractServiceRegistryImpl.initializeService(AbstractServiceRegistryImpl.java:237) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
    at org.hibernate.service.internal.AbstractServiceRegistryImpl.getService(AbstractServiceRegistryImpl.java:214) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
    at org.hibernate.id.factory.internal.DefaultIdentifierGeneratorFactory.injectServices(DefaultIdentifierGeneratorFactory.java:175) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
    at org.hibernate.service.internal.AbstractServiceRegistryImpl.injectDependencies(AbstractServiceRegistryImpl.java:286) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
    at org.hibernate.service.internal.AbstractServiceRegistryImpl.initializeService(AbstractServiceRegistryImpl.java:243) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
    at org.hibernate.service.internal.AbstractServiceRegistryImpl.getService(AbstractServiceRegistryImpl.java:214) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
    at org.hibernate.boot.internal.InFlightMetadataCollectorImpl.<init>(InFlightMetadataCollectorImpl.java:173) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
    at org.hibernate.boot.model.process.spi.MetadataBuildingProcess.complete(MetadataBuildingProcess.java:127) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
    at org.hibernate.jpa.boot.internal.EntityManagerFactoryBuilderImpl.metadata(EntityManagerFactoryBuilderImpl.java:1460) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
    at org.hibernate.jpa.boot.internal.EntityManagerFactoryBuilderImpl.build(EntityManagerFactoryBuilderImpl.java:1494) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
    at org.springframework.orm.jpa.vendor.SpringHibernateJpaPersistenceProvider.createContainerEntityManagerFactory(SpringHibernateJpaPersistenceProvider.java:58) ~[spring-orm-5.3.22.jar:5.3.22]
    at org.springframework.orm.jpa.LocalContainerEntityManagerFactoryBean.createNativeEntityManagerFactory(LocalContainerEntityManagerFactoryBean.java:365) ~[spring-orm-5.3.22.jar:5.3.22]
    at org.springframework.orm.jpa.AbstractEntityManagerFactoryBean.buildNativeEntityManagerFactory(AbstractEntityManagerFactoryBean.java:409) ~[spring-orm-5.3.22.jar:5.3.22]
    at org.springframework.orm.jpa.AbstractEntityManagerFactoryBean.afterPropertiesSet(AbstractEntityManagerFactoryBean.java:396) ~[spring-orm-5.3.22.jar:5.3.22]
    at org.springframework.orm.jpa.LocalContainerEntityManagerFactoryBean.afterPropertiesSet(LocalContainerEntityManagerFactoryBean.java:341) ~[spring-orm-5.3.22.jar:5.3.22]
    at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.invokeInitMethods(AbstractAutowireCapableBeanFactory.java:1863) ~[spring-beans-5.3.22.jar:5.3.22]
    at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.initializeBean(AbstractAutowireCapableBeanFactory.java:1800) ~[spring-beans-5.3.22.jar:5.3.22]
    at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.doCreateBean(AbstractAutowireCapableBeanFactory.java:620) ~[spring-beans-5.3.22.jar:5.3.22]
    at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.createBean(AbstractAutowireCapableBeanFactory.java:542) ~[spring-beans-5.3.22.jar:5.3.22]
    at org.springframework.beans.factory.support.AbstractBeanFactory.lambda$doGetBean$0(AbstractBeanFactory.java:335) ~[spring-beans-5.3.22.jar:5.3.22]
    at org.springframework.beans.factory.support.DefaultSingletonBeanRegistry.getSingleton(DefaultSingletonBeanRegistry.java:234) ~[spring-beans-5.3.22.jar:5.3.22]
    at org.springframework.beans.factory.support.AbstractBeanFactory.doGetBean(AbstractBeanFactory.java:333) ~[spring-beans-5.3.22.jar:5.3.22]
    at org.springframework.beans.factory.support.AbstractBeanFactory.getBean(AbstractBeanFactory.java:208) ~[spring-beans-5.3.22.jar:5.3.22]
    at org.springframework.context.support.AbstractApplicationContext.getBean(AbstractApplicationContext.java:1154) ~[spring-context-5.3.22.jar:5.3.22]
    at org.springframework.context.support.AbstractApplicationContext.finishBeanFactoryInitialization(AbstractApplicationContext.java:908) ~[spring-context-5.3.22.jar:5.3.22]
    at org.springframework.context.support.AbstractApplicationContext.refresh(AbstractApplicationContext.java:583) ~[spring-context-5.3.22.jar:5.3.22]
    at org.springframework.boot.web.servlet.context.ServletWebServerApplicationContext.refresh(ServletWebServerApplicationContext.java:147) ~[spring-boot-2.7.2.jar:2.7.2]
    at org.springframework.boot.SpringApplication.refresh(SpringApplication.java:734) ~[spring-boot-2.7.2.jar:2.7.2]
    at org.springframework.boot.SpringApplication.refreshContext(SpringApplication.java:408) ~[spring-boot-2.7.2.jar:2.7.2]
    at org.springframework.boot.SpringApplication.run(SpringApplication.java:308) ~[spring-boot-2.7.2.jar:2.7.2]
    at org.springframework.boot.SpringApplication.run(SpringApplication.java:1306) ~[spring-boot-2.7.2.jar:2.7.2]
    at org.springframework.boot.SpringApplication.run(SpringApplication.java:1295) ~[spring-boot-2.7.2.jar:2.7.2]
    at com.kgh.membership.MembershipApplication.main(MembershipApplication.java:10) ~[main/:na]

2022-08-02 01:02:07.312 ERROR 30126 --- [           main] j.LocalContainerEntityManagerFactoryBean : Failed to initialize JPA EntityManagerFactory: Unable to create requested service [org.hibernate.engine.jdbc.env.spi.JdbcEnvironment]
2022-08-02 01:02:07.315  WARN 30126 --- [           main] ConfigServletWebServerApplicationContext : Exception encountered during context initialization - cancelling refresh attempt: org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'entityManagerFactory' defined in class path resource [org/springframework/boot/autoconfigure/orm/jpa/HibernateJpaConfiguration.class]: Invocation of init method failed; nested exception is org.hibernate.service.spi.ServiceException: Unable to create requested service [org.hibernate.engine.jdbc.env.spi.JdbcEnvironment]
2022-08-02 01:02:07.321  INFO 30126 --- [           main] o.apache.catalina.core.StandardService   : Stopping service [Tomcat]
2022-08-02 01:02:07.340  INFO 30126 --- [           main] ConditionEvaluationReportLoggingListener : 

Error starting ApplicationContext. To display the conditions report re-run your application with 'debug' enabled.
2022-08-02 01:02:07.361 ERROR 30126 --- [           main] o.s.boot.SpringApplication               : Application run failed

org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'entityManagerFactory' defined in class path resource [org/springframework/boot/autoconfigure/orm/jpa/HibernateJpaConfiguration.class]: Invocation of init method failed; nested exception is org.hibernate.service.spi.ServiceException: Unable to create requested service [org.hibernate.engine.jdbc.env.spi.JdbcEnvironment]
    at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.initializeBean(AbstractAutowireCapableBeanFactory.java:1804) ~[spring-beans-5.3.22.jar:5.3.22]
    at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.doCreateBean(AbstractAutowireCapableBeanFactory.java:620) ~[spring-beans-5.3.22.jar:5.3.22]
    at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.createBean(AbstractAutowireCapableBeanFactory.java:542) ~[spring-beans-5.3.22.jar:5.3.22]
    at org.springframework.beans.factory.support.AbstractBeanFactory.lambda$doGetBean$0(AbstractBeanFactory.java:335) ~[spring-beans-5.3.22.jar:5.3.22]
    at org.springframework.beans.factory.support.DefaultSingletonBeanRegistry.getSingleton(DefaultSingletonBeanRegistry.java:234) ~[spring-beans-5.3.22.jar:5.3.22]
    at org.springframework.beans.factory.support.AbstractBeanFactory.doGetBean(AbstractBeanFactory.java:333) ~[spring-beans-5.3.22.jar:5.3.22]
    at org.springframework.beans.factory.support.AbstractBeanFactory.getBean(AbstractBeanFactory.java:208) ~[spring-beans-5.3.22.jar:5.3.22]
    at org.springframework.context.support.AbstractApplicationContext.getBean(AbstractApplicationContext.java:1154) ~[spring-context-5.3.22.jar:5.3.22]
    at org.springframework.context.support.AbstractApplicationContext.finishBeanFactoryInitialization(AbstractApplicationContext.java:908) ~[spring-context-5.3.22.jar:5.3.22]
    at org.springframework.context.support.AbstractApplicationContext.refresh(AbstractApplicationContext.java:583) ~[spring-context-5.3.22.jar:5.3.22]
    at org.springframework.boot.web.servlet.context.ServletWebServerApplicationContext.refresh(ServletWebServerApplicationContext.java:147) ~[spring-boot-2.7.2.jar:2.7.2]
    at org.springframework.boot.SpringApplication.refresh(SpringApplication.java:734) ~[spring-boot-2.7.2.jar:2.7.2]
    at org.springframework.boot.SpringApplication.refreshContext(SpringApplication.java:408) ~[spring-boot-2.7.2.jar:2.7.2]
    at org.springframework.boot.SpringApplication.run(SpringApplication.java:308) ~[spring-boot-2.7.2.jar:2.7.2]
    at org.springframework.boot.SpringApplication.run(SpringApplication.java:1306) ~[spring-boot-2.7.2.jar:2.7.2]
    at org.springframework.boot.SpringApplication.run(SpringApplication.java:1295) ~[spring-boot-2.7.2.jar:2.7.2]
    at com.kgh.membership.MembershipApplication.main(MembershipApplication.java:10) ~[main/:na]
Caused by: org.hibernate.service.spi.ServiceException: Unable to create requested service [org.hibernate.engine.jdbc.env.spi.JdbcEnvironment]
    at org.hibernate.service.internal.AbstractServiceRegistryImpl.createService(AbstractServiceRegistryImpl.java:275) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
    at org.hibernate.service.internal.AbstractServiceRegistryImpl.initializeService(AbstractServiceRegistryImpl.java:237) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
    at org.hibernate.service.internal.AbstractServiceRegistryImpl.getService(AbstractServiceRegistryImpl.java:214) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
    at org.hibernate.id.factory.internal.DefaultIdentifierGeneratorFactory.injectServices(DefaultIdentifierGeneratorFactory.java:175) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
    at org.hibernate.service.internal.AbstractServiceRegistryImpl.injectDependencies(AbstractServiceRegistryImpl.java:286) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
    at org.hibernate.service.internal.AbstractServiceRegistryImpl.initializeService(AbstractServiceRegistryImpl.java:243) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
    at org.hibernate.service.internal.AbstractServiceRegistryImpl.getService(AbstractServiceRegistryImpl.java:214) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
    at org.hibernate.boot.internal.InFlightMetadataCollectorImpl.<init>(InFlightMetadataCollectorImpl.java:173) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
    at org.hibernate.boot.model.process.spi.MetadataBuildingProcess.complete(MetadataBuildingProcess.java:127) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
    at org.hibernate.jpa.boot.internal.EntityManagerFactoryBuilderImpl.metadata(EntityManagerFactoryBuilderImpl.java:1460) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
    at org.hibernate.jpa.boot.internal.EntityManagerFactoryBuilderImpl.build(EntityManagerFactoryBuilderImpl.java:1494) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
    at org.springframework.orm.jpa.vendor.SpringHibernateJpaPersistenceProvider.createContainerEntityManagerFactory(SpringHibernateJpaPersistenceProvider.java:58) ~[spring-orm-5.3.22.jar:5.3.22]
    at org.springframework.orm.jpa.LocalContainerEntityManagerFactoryBean.createNativeEntityManagerFactory(LocalContainerEntityManagerFactoryBean.java:365) ~[spring-orm-5.3.22.jar:5.3.22]
    at org.springframework.orm.jpa.AbstractEntityManagerFactoryBean.buildNativeEntityManagerFactory(AbstractEntityManagerFactoryBean.java:409) ~[spring-orm-5.3.22.jar:5.3.22]
    at org.springframework.orm.jpa.AbstractEntityManagerFactoryBean.afterPropertiesSet(AbstractEntityManagerFactoryBean.java:396) ~[spring-orm-5.3.22.jar:5.3.22]
    at org.springframework.orm.jpa.LocalContainerEntityManagerFactoryBean.afterPropertiesSet(LocalContainerEntityManagerFactoryBean.java:341) ~[spring-orm-5.3.22.jar:5.3.22]
    at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.invokeInitMethods(AbstractAutowireCapableBeanFactory.java:1863) ~[spring-beans-5.3.22.jar:5.3.22]
    at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.initializeBean(AbstractAutowireCapableBeanFactory.java:1800) ~[spring-beans-5.3.22.jar:5.3.22]
    ... 16 common frames omitted
Caused by: org.hibernate.HibernateException: Access to DialectResolutionInfo cannot be null when 'hibernate.dialect' not set
    at org.hibernate.engine.jdbc.dialect.internal.DialectFactoryImpl.determineDialect(DialectFactoryImpl.java:100) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
    at org.hibernate.engine.jdbc.dialect.internal.DialectFactoryImpl.buildDialect(DialectFactoryImpl.java:54) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
    at org.hibernate.engine.jdbc.env.internal.JdbcEnvironmentInitiator.initiateService(JdbcEnvironmentInitiator.java:138) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
    at org.hibernate.engine.jdbc.env.internal.JdbcEnvironmentInitiator.initiateService(JdbcEnvironmentInitiator.java:35) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
    at org.hibernate.boot.registry.internal.StandardServiceRegistryImpl.initiateService(StandardServiceRegistryImpl.java:101) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
    at org.hibernate.service.internal.AbstractServiceRegistryImpl.createService(AbstractServiceRegistryImpl.java:263) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
    ... 33 common frames omitted
```

- shooting:
    
    
    제대로된 h2 데이터베이스가 생성되지 못해서 생긴 문제이다. 해당 지정되는 경로에 membership.mv.db 라는 파일이 생성되어야 하는데 해당되는 경로를 찾지못한게 문제가 되었다.
    
    그래서 다음과 같이 해결할 수 있었다.
    
    application.yml 파일에서 다음과 같이 url을 지정해준다.
    
    ```jsx
    spring:
      datasource:
            url: jdbc:h2:~/membership
        username: sa
        password:
        driver-class-name: org.h2.Driver
      jpa:
        hibernate:
          ddl-auto: create
        properties:
          hibernate:
            format_sql: true
    logging:
      level:
        org.hibernate.SQL: debug
    ```
    
    url을 다음과 같이 설정하여 해당되는 경로문제를 해결할 수 있었다. 해결되니 ~/(홈경로)에 membership.mv.db파일이 생성되었다. 하지만 [localhost:8080/h2-console](http://localhost:8080/h2-console) 경로로 접속하니 whitelabel 에러가 발생하여 접속이 불가하였다.
    
    찾아보니
    
    ```jsx
    implementation 'org.springframework.boot:spring-boot-devtools'
    ```
    
    devtools 의존성을 추가해주지 않아 생긴 문제였다. 해당 의존성을 추가해주고, [localhost:8080/h2-console로](http://localhost:8080/h2-console로) 접속하니 바로 해결할 수 있었다.

