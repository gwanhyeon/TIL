# log4j2

springboot web에서 내장되어있는 logback과 log4j를 고민중 멀티쓰레드 환경에서 비동기 로깅을 처리 할 수 있는 log4j2로 환경을 구성.

# log4j2 특징

자동 리로드 기능과 필터리 기능을 제공합니다. logback과 차이점은 Apache에 따르면 멀티 쓰레드 환경에서 비동기 로거(Async Logger)의 경우 Log4j 1.x 및 Logback보다 처리량이 18배 더 높고 대기 시간이 훨씬 더 짧다. 아래 그래프에서 성능 차이를 확인 해볼수 있다. 그리고 람다 표현식과 사용자 정의 로그 레벨도 지원합니다.

# log4j2 xml 설정

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Configuration status="INFO">
    <Properties>
        <Property name="logFileName">membershipDev</Property>
        <Property name="consoleLayout">%style{%d{ISO8601}}{black} %highlight{%-5level }[%style{%t}{bright,blue}] %style{%C{1.}}{bright,yellow}: %msg%n%throwable</Property>
        <Property name="fileLayout">%d [%t] %-5level %c(%M:%L) - %m%n</Property>
    </Properties>

    <Appenders>
        <Console name="console" target="SYSTEM_OUT">
            <PatternLayout pattern="${consoleLayout}" />
        </Console>
        <RollingFile name="saveFile" fileName="logs/${logFileName}.log" filePattern="logs/${logFileName}.%d{yyyy-MM-dd-hh}.log">

            <PatternLayout pattern="${fileLayout}" />
            <Policies>
                <TimeBasedTriggeringPolicy modulate="true" interval="1" /><!-- 시간별 로그 파일 생성-->
            </Policies>
            <DefaultRolloverStrategy max="7" fileIndex="max" >
                <Delete basePath = "logs" maxDepth = "1">
                    <!-- 3일이 경과한 로그파일은 자동 삭제 -->
                    <IfLastModified age = "3d"/>
                </Delete>
            </DefaultRolloverStrategy>
        </RollingFile>
    </Appenders>
    <Loggers>

        <!-- 스프링 프레임워크에서 찍는건 level을 info로 설정 -->
        <logger name="org.springframework" level="INFO" additivity="false" >
            <AppenderRef ref="console" />
            <AppenderRef ref="saveFile" />
        </logger>

        <!-- rolling file에는 debug, console에는 info 분리하여 처리 가능하다. -->
        <logger name="com.kgh.membership" additivity="true" >
            <AppenderRef ref="console" level="info" />
            <AppenderRef ref="saveFile" level="debug" />
        </logger>

        <Root level="INFO">
            <AppenderRef ref="console"/>
            <AppenderRef ref="saveFile"/>
        </Root>
    </Loggers>
</Configuration>

```


# log4j2 level

trace < debug < info < warn < error.

# log4j2 프로젝트 정책

```xml
logger.info("info = {}", "info contents");

logger.info("debug = {}", "debug contents");

logger.error("error = {}", "error contents");

logger.warn("warn = {}", "error contents");
```

프로젝트시 기존 console info에 대한 내용을 찍을때와 warn, error를 각각 구분해서 확인 할 수 있도록한다.

> 추가

logs 경로에서 `$tail -1000f membershipDev.log` 명령어를 통하여 1000줄까지 파일이 업데이트되고 있는 로그를 실시간으로 확인 할 수 있도록한다.