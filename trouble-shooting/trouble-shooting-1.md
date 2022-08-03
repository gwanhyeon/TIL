# trouble-shooting-1

> trouble:

```java
**************************
APPLICATION FAILED TO START
***************************

Description:

Failed to configure a DataSource: 'url' attribute is not specified and no embedded datasource could be configured.

Reason: Failed to determine a suitable driver class


Action:

Consider the following:
    If you want an embedded database (H2, HSQL or Derby), please put it on the classpath.
    If you have database settings to be loaded from a particular profile you may need to activate it (no profiles are currently active).


Process finished with exit code 1
```

드라이버 클래스를 제대로 찾지 못하는 에러가 발생하였다. 처음에는 jdk 문제인것으로 파악하여 프로젝트 jdk11로 변경하여 빌드를 수행하였는데 실패하였다. 다른 방법을 고안하다가 의존성 문제가 있을 것이라 판단하에 아래와 같은 문제가 발생하였다.

> shooting:

```xml
implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
```

jpa dependency를 추가하였는데, jpa는 해당되는 db dependency가 지정되어야하는데 그러지 못하였다.
따라서, 개발시에 사용할 h2 databases를 사용하기 위해 해당 의존성을 추가해주었다.

```xml
runtimeOnly 'com.h2database:h2'
```

해당 h2 데이터베이스를 지정해주니 정상적으로 컴파일이 동작하는것을 알 수 있었다.
