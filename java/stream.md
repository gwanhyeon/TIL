# Java 8 Stream
Java8부터 지원하는  Stream에 대해서 살펴보겠습니다. Stream은 컬렉션, 배열 등 요소에 관한 참조와 반복을 쉽게 처리할 수 있는 기능입니다.
if문 대신에 stream의 filter를 통하여 분기처리를 쉽게 처리할 수 있고 직관적인 변형이 가능하게 됩니다.

# Stream의 구조

Stream의 구조는 세가지로 나눌 수 있습니다.

- 스트림 생성
- 스트림 중간 연산
- 스트림 최종 연산

`[객체집합.생성.중간연산.최종연산]`으로 나눌 수 있습니다.

# Stream의 특징

- Stream은 데이터를 변경하지 않고 원본 데이터로부터 데이터를 읽기만 할 뿐, 원본데이터 자체를 변경하지 않는다.
- Stream은 일회용이다. Stream을 한번 사용하게 되면 닫혀서 재사용이 불가능하다. 그리고 필요하다면 정렬된 결과를 컬렉션이나 배열에 담아 반환할 수 있다
- Stream은 작업을 내부 반복으로 처리한다. .Stream을 사용하면 작업이 간결할 수 있는 비결중 하나가 바로 내부 반복이다. 내부 반복이라는 것은 반복문을 메서드 내부에 숨길 수 있다는 것을 뜻한다.



# Stream 생성 과정

### 1.컬렉션
```java
// Create stream from collection
List<Integer> collectionsList = new ArrayList<>();
collectionsList.add(1);
collectionsList.add(2);
collectionsList.stream()
.forEach(System.out::println);
```
### 2.배열
```java
 // Create stream from arrays
String[] arr = new String[] {"one","two"};
Stream<String> stream = Arrays.stream(arr);
stream.forEach(e -> System.out.print(e));
System.out.println();
```
### 3.가변 매개변수
```java
// Create a stream using only a specific part of the array
Stream<String> stream2 = Arrays.stream(arr, 1,3);
stream2.forEach(e -> System.out.print(e + " "));
```
### 4.지정된 범위의 연속된 정수
```java
// Create streams from variable parameters 
Stream<Double> stream3 = Stream.of(4.2, 2.5, 3.1, 1.9);
stream.forEach(System.out::println);

// Create streams from consecutive integers in a specified range
IntStream stream4 = IntStream.range(1,4);
stream4.forEach(e -> System.out.println(e + " "));
IntStream stream5 = IntStream.rangeClosed(1, 4);
stream5.forEach(e -> System.out.println(e + " "));
```java
### 5.특정 타입의 난수들

```java	
// Create a stream of random numbers of a particular type
IntStream stream6 = new Random().ints(4);
stream.forEach(System.out::println);
```
### 6.람다표현식

```java
// create lambda Expression
Stream<Integer> stream7 = Stream.iterate(2, n -> n+2);
stream7.forEach(System.out::println);
```
### 7. 파일
```java   
// Create stream from files 
Stream<String> stream8 = Files.lines(Paths.get("file.txt"));
```
### 8.빈 스트림 
```java   
// Create an empty stream
 Stream<Object> stream9 = Stream.empty();
System.out.println(stream9.count());
```
# Stream 중간 연산 과정

### 1. 필터링 : filter(), distinct()
```java
// stream filter(), distinct
IntStream stream1 = IntStream.of(10,20,30,40,50);
IntStream stream2 = IntStream.of(20,40,60,80,100);

 // stream 홀수만 골라내기
stream2.filter(n -> n % 2 != 0).forEach(o -> System.out.println("o : " + o));
```
### 2. 변환 : map(), flatMap()
```
// stream 중복된 요소를 제거함
stream1.distinct().forEach(e -> System.out.print(e + " "));
System.out.println();

// map(), flatMap
Stream<String> stream3 = Stream.of("HTML", "CSS", "JAVA", "JAVASCRIPT");
stream3.map(s -> s.toLowerCase()).forEach(System.out::println);

// 여러 문자열 스트림 변환 
String[] arrList = {"hh", "ee", "ll","ll", "oo"};		Stream<String> stream4 = Arrays.stream(arrList);		stream4.flatMap(s -> Stream.of(s.split(" +"))).forEach(System.out::println);
```

### 3. 제한 : limit(), skip()
```java
  // limit(), skip()
IntStream stream5 = IntStream.range(0, 10);
IntStream stream6 = IntStream.range(0, 10);
IntStream stream7 = IntStream.range(0, 10);

stream5.skip(4).forEach(n -> System.out.print(n + " "));
System.out.println();
stream6.limit(5).forEach(n -> System.out.print(n + " "));
System.out.println();
stream7.skip(3).limit(5).forEach(n -> System.out.print(n + " "));
```
### 4. 정렬 : sorted()
```java
// sorted - desc
Stream<String> stream8 = Stream.of("kgh", "kim");
Stream<String> stream9 = Stream.of("kgh1", "gwanhyeon");
stream8.sorted().forEach(s -> System.out.println("s : " + s));
	
// sorted - asc
System.out.println();
stream9.sorted(Comparator.reverseOrder()).forEach(s -> System.out.print("s : " + s));
```
### 5. 연산 결과 확인: peek()
Java8 에서 stream 에는 두가지의 반복문이 사용가능한데 peek() 과 forEach() 함수를 제공합니다. forEach는 return 값이 void 라서 최종처리메소드로 쓰일 수 있지만 peek은 stream 을 return 해서 불가능합니다.
```java
Member member1 = new Member("MuMu", 30);
Member member2 = new Member("MuNu", 40);
Member member3 = new Member("MuLu", 50);

List<Member> members = Lists.newArrayList(member1, member2, member3);

members.stream()
.peek(m -> System.out.println("My name is " + m.name))
.allMatch(m -> m.equals(member1));

members.stream()
.peek(m -> System.out.println("My name is " + m.name))
.allMatch(m -> m.equals(member2)); 

members.stream() 
.peek(m -> System.out.println("My name is " + m.name))
.allMatch(m -> m.equals(member3));
```

# Stream 최종 연산 과정
### 1.  출력 : forEach()
```java
// forEach()
Stream<String> stream = Stream.of("one", "two");
stream.forEach(System.out::println);
```
### 2.  소모 : reduce()

```java
   // reduce()
Stream<String> stream1 = Stream.of("One", "Two");
Stream<String> stream2 = Stream.of("One", "TWo");
Optional<String> result1 = stream1.reduce((s1,s2) -> s1 + " ++ " + s2);
result1.ifPresent(System.out::println);
String result2 = stream2.reduce("Start",(s1, s2) -> s1 + " ++ " + s2);
System.out.println(result2);
```

### 3.  검색 : findFirst(), findAny()
```java
 // findFist(), findAny()
IntStream stream3 = IntStream.of(10,20,30,40,50);	
IntStream stream4 = IntStream.of(20,30,40,50,60);
```
### 4.  검사 : anyMatch(), allMatch(), noneMatch()
```java
// anyMatch, allMatch, noneMatch()
System.out.println(stream3.anyMatch(n -> (n > 80) ));
System.out.println(stream4.allMatch(n -> (n > 80) ));
```
### 5.  통계 : count(), min(), max()
```java
// count(), min(), max()
IntStream stream5 = IntStream.of(30,90,120);
IntStream stream6 = IntStream.of(30,90,120);
System.out.println(stream5.count());
System.out.println(stream6.max().getAsInt());
```

### 6.  연산 : sum(), average()
```java
// sum(), average()
IntStream stream7 = IntStream.of(100,200);
DoubleStream stream8 = DoubleStream.of(10.5, 20.5);
System.out.println(stream7.sum());
System.out.println(stream8.average().getAsDouble());
```

### 7.  수집 : collect()
```java
// collect()
Stream<String> stream9 = Stream.of("One", "Two");
List<String> list = stream9.collect(Collectors.toList());
Iterator<String> iter = list.iterator();
while(iter.hasNext()) {
	System.out.println(iter.next() +  " ");
}

// Collectors 클래스의 partitioningBy()
Stream<String> stream10 = Stream.of("kgh", "kim");
Map<Boolean, List<String>> partition = stream10.collect(Collectors.partitioningBy(s -> (s.length() % 2) == 0 ));

List<String> oodLengthList = partition.get(false);
System.out.println(oodLengthList);
List<String> evenLengthList = partition.get(true);
System.out.println(evenLengthList);
```