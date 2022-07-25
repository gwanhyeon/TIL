# server.xml의 구조 

### server.xml 디렉터리 경로
  
`$CATALINA_BASE/conf` 경로에 존재하는 server.xml 파일은 주요 설정 파일 및 Tomcat의 구성요소, 가상호스트 구성요소를 확인할 수 있다.

### server.xml 구성요소

`<Connector>, <Server>, <Service>, <Engine>, <Host>` 의 구성요소를 가지고 있다.

### Server(org.apache.catalina.Server)

최상위 element로 shutdown 요청 처리를 위한 `address`와 `port` 속성을 가지고 있다.

각각의 shutdown 요청을 받기위해 listen하는 IP address와 포트를 설정하며 기본 값은 `localhost:8005`

```xml
<Server port="8005" shutdown="SHUTDOWN">
```

port를 -1로 설정할 경우 shutdown 포트기능을 사용하지 않는다. shutdown 속성은 shutdown 명령어(패스워드)를 설정한다.

### Service(org.apache.catalina.Service)

`<Service> 하위에 있으며 <Connector>의 모음`

> Service의 속성

- className
- name


```xml
<Service name="Catalina">
```

### Engine(org.apache.catalina.Engine)

Engine Container의 기본 클래스는 o.a.catalina.StandardEngine이며 Engine 엘리먼트는 `name, defaultHost, jvmRoute` 속성을 갖고 있다.

> Engine 엘리먼트의 특징

- `name` <Engine>의 이름
- `defaultHost` <Engine>하위에 속한 <Host>가운데 하나이며, 어떤 도 처리하지 않는 요청을 처리한다.
- `jvmRoute` Apache HTTP Server 등 front-end에 위치한 Load Balancer가 여러 Tomcat 인스턴스 구분을 위해 사용. 특히 클러스터 그룹 내의 jvmRoute는 각 인스턴스마다 고유해야 한다.

```xml
<Engine name="Catalina" defaultHost="localhost">
```

### Host(org.apache.catalin.Hst)

Host Container는 가상 호스트 기능을 제공하며 기본 클래스는 o.a.catalina.standardHost이다.

```xml
<Host name="localhost" appBase="webapps" unpackWARs="true" autoDeploy="true">
```

> Host 엘리먼트 특징

- `name` <Host>의 이름은 name 속성을 통해 설정한다. 상위 <Engine>내에 2개 이상의 <Host>가 구성되어 있다면 그 중 1개 <Host>가 <Engine>의 defaultHost값이 되어야 한다.
- `appBase` <Host>의 애플리케이션 디렉터리 "/"를 포함한 절대 경로, 혹은 $CATALINA_BASE의 상대 경로로 설정하며 기본은 wbapps이다.


### Context

Context는 <Host>내에 배포된 어플리캐이션이다.

```xml
<Host name="localhost" appBase="webapps" unpackWARs="true" autoDeploy="true">
  <Context docBase="특정경로" path="/application1" reloadable="true">
  </Context>
```

> Context 설정 방법

1. 각 애플리케이션의 META-INF/context.xml을 통해 설정한다. 만일 copyXML 속성이 true이면 context.xml파일을 자동으로 $CATALINA_BASE/conf/<Engie>/<Host> 디렉터리 아래의 [애플리케이션].xml 파일로 복사한다.

2. $CATALINA_BSAE/conf/<Engie>/<Host> 디렉터리 하위에 [애플리케이션].xml을 만들어 설정한다. 이 때 애플리케이션 Context Path와 같다.

3. $CATALINA_BASE/conf/server.xml의 <Host>안에 설정한다. (권장되지 않음)

$CATALINA_BASE/conf/context.xml 파일은 Global context 파일이기 때문에 Tomcat 내의 모든 애플리케이션이 공통으로 사용한다.
$CATALINA_BASE/conf/<Engie>/<Host>/context.xml default 파일은 <Host>의 Global Context파일이기 때문에 <Host>하위 모든 애플리케이션이 사용한다.


> reference

https://exhibitlove.tistory.com/312
https://cornswrold.tistory.com/347





