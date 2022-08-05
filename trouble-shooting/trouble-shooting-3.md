> trouble:

`Cause: invalid source release: 11`

Gradle의 jvm설정이 11 이하 버전이고 bulid.gradle에 sourceCompatibility의 설정이 11일 경우 발생

> shooting:
> 
1. sourceCompatibility 값을 gradle의 설정 jvm값으로 변경한다.

2. gradle jvm설정을 11로 올린다.

`setting -> build, excution, deployment -> bulid tools -> gradle -> gradle projects -> gradle jvm`

컴파일 시점의 JDK 버전과 Gradle JVM JDK 버전을 맞추어준다. 현재 JDK11 버전을 사용하고 있었기 때문에 컴파일 JDK, Gradle JDK를 모두 11버전으로 변경해주었다.
