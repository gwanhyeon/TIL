# memory leak

메모리 누수(memory leak)란?
CS 의미로 살펴볼 때, 컴퓨터 프로그램이 필요하지 않은 메모리를 계속 점유하고 있는 현상이다.

 

할당된 메모리를 사용한 다음 반환하지 않는 것이 누적되면 메모리가 낭비된다. 즉, 더 이상 불필요한 메모리가 해제되지 않으면서 메모리 할당을 잘못 관리할 때 발생한다.

 

일부 서적에서 메모리 손실이라는 용어로 뜻을 옮기기도 하지만 leak라는 표현은 단순히 잃는 것 이상의 개념이므로 누수라는 표현이 더 정확하다.

자바에서 메모리 누수(memory leak)
더 이상 사용되지 않는 객체들이 가비지 컬렉터에 의해 회수되지 않고 계속 누적이 되는 현상을 말한다.

Old 영역에 계속 누적된 객체로 인해 Major GC가 빈번하게 발생하게 되면서, 프로그램 응답속도가 늦어지면서 성능 저하를 불러온다. 이는 결국 OutOfMemory Error로 프로그램이 종료되게 된다.

 

가비지 컬렉션을 통해 소멸 대상이 되는 객체가 되기 위해서는 어떠한 reference 변수에서 가르키지 않아야 한다.
다 쓴 객체에 대한 참조를 해제하지 않으면 가비지 컬렉션의 대상이 되지 않아 계속 메모리가 할당 되는 메모리 누수 현상이 발생 된다.

 

GC가 되지 않는 루트 참조 객체는 크게 3가지다.

 

# 1. Static 변수에 의한 객체 참조

static는 GC에 대상이 되지 않는다. Static 변수는 클래스가 생성될 때 메모리를 할당 받고 프로그램 종료 시점에 반환되므로 사용하지 않고 있어도 메모리가 할당되어 있다.  잘 활용하면 성능을 향상시킬 수 있지만, 사용하지 않는데 계속 할당 되기만 한다면 GC가 되지 않아 메모리 릭으로 이어져 시스템 자체가 돌아갈 수 없는 상태에 이를 수 있다.
2. 모든 현재 자바 스레드 스택내의 지역 변수, 매개 변수에 의한 객체 참조

자바에서 현재 실행중인 (각 스레드별로) 모든 메소드내에 선언된 지역 변수와 매개변수에 의해 참조되는 객체와  그 객체로부터 직간접적으로 참조되는 모든 객체는 참조되어 사용될 가능성이 있으며, 이 뿐만 아니라 caller 메소드로 return된 후에는 caller 메소드에서 참조하고 있는 지역변수, 매개변수에 의해 참조되는 객체와 객체로부터 직간접적으로 참조되는 모든 객체 또한, GC되지 않고 참조되어 사용될 가능성이 있다.
따라서, 각 자바 스레드의 스택 프레임내에 있는 모든 지역변수와 매개 변수에 의해 참조되는 객체와 그 객체로부터 직간접적으로 참조되는 모든 객체들이 참조되어 사용될 가능성이 있다는 것이다.
3. JNI 프로그램에 의해 동적으로 만들어지고 제거되는 JNI global 객체 참조

 

그 외 또 여러가지 방법으로 메모리 누수(memory leak)가 발생하는 패턴들이 있다.

 

# 1. Integer, Long 같은 래퍼 클래스(Wrapper)를 이용하여, 무의미한 객체를 생성하는 경우

public class Adder {
       publiclong addIncremental(long l)
       {
              Long sum=0L;
               sum =sum+l;
               return sum;
       }
       public static void main(String[] args) {
              Adder adder = new Adder();
              for(long ;i<1000;i++)
              {
                     adder.addIncremental(i);
              }
       }
}
long 대신 Long을 사용함으로써 , 오토 박싱으로 인해 sum=sum+l;에서 매 반복마다 새 개체를 생성하므로 1000개의 불필요한 객체가 생성된다.

 

 

# 2. 맵에 캐쉬 데이터를 선언하고 해제하지 않는 경우

import java.util.HashMap;
import java.util.Map;
public class Cache {
       private Map<String,String> map= new HashMap<String,String>();
       publicvoid initCache()
       {
              map.put("Anil", "Work as Engineer");
              map.put("Shamik", "Work as Java Engineer");
              map.put("Ram", "Work as Doctor");
       }
       public Map<String,String> getCache()
       {
              return map;
       }
       publicvoid forEachDisplay()
       {
              for(String key : map.keySet())
              {
                String val = map.get(key);                 
                System.out.println(key + " :: "+ val);
              }
       }
       public static void main(String[] args) {            
              Cache cache = new Cache();
              cache.initCache();
              cache.forEachDisplay();
       }
}
캐시에 직원과 직종을 넣었지만, 캐시를 지우지 않았다. 객체가 더 이상 사용되지 않을 때도 Map에 강력한 참조가 있기 때문에 GC가 되지 않는다.  

 

캐시의 항목이 더 이상 필요하지 않을 떄는 캐시를 지워주는 것이 바람직하다. 

 

또한 WeakHashMap으로 캐시를 초기화 할 수 있다. WeakHashMap의 장점은 키가 다른 객체에서 참조되지 않는 경우 해당 항목이 GC가 된다.

 

하지만, 캐시에 저장된 값을 재사용하려면 해당 키가 다른 객체에 의해 참조되지 않을 수 있으므로 항목이 GC되고 해당 값이 사라질 수 있기 때문에 주의하여야 한다.

 

 

# 3. 스트림 객체를 사용하고 닫지 않는 경우

try
{
  Connection con = DriverManager.getConnection();
  …………………..
    con.close();
}

Catch(exception ex)
{
}
try 블록에서 연결 리소스를 닫으므로 예외가 발생하는 경우 연결이 닫히지 않는다. 따라서이 연결이 풀로 다시 돌아 오지 않기 때문에 메모리 누수가 발생한다. 또한 닫아지지 않아서 데드락이 발생할 가능 성이 크다.

항상 finally 블록에 닫는 내용을 넣거나, TryWhitResource를 사용하자.

 

# 4. 맵의 키를 사용자 객체로 정의하면서 equals(), hashcode()를 재정의 하지 않아서 같은 키로 착각하여 데이터가 계속 쌓이게 되는 경우

import java.util.HashMap;
import java.util.Map;

public class CustomKey {
       public CustomKey(String name)
       {
              this.name=name;
       }
       
       private String name;
       
       publicstaticvoid main(String[] args) {
              Map<CustomKey,String> map = new HashMap<CustomKey,String>();
              map.put(new CustomKey("Shamik"), "Shamik Mitra");
              String val = map.get(new CustomKey("Shamik"));
              System.out.println("Missing equals and hascode so value is not accessible from Map " + val);
       }
}
equals () 및 hashcode()를 재정의 해주지 않아서, 버킷에 계속 데이터가 쌓여 메모리 누수가 발생한다.

 

# 5. 맵의 키를 사용자 객체로 정의하면서 equals(), hashcode()를 재정의 하였지만, 키값이 불변(Immutable) 데이터가 아니라서 데이터 비교시 계속 변하게 되는 경우

import java.util.HashMap;
import java.util.Map;

public class MutableCustomKey {
    public MutableCustomKey(String name) {
        this.name = name;
    }

    private String name;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    @Override
    public int hashCode() {
        final int prime = 31;
        int result = 1;
        result = prime * result + ((name == null) ? 0 : name.hashCode());
        return result;
    }

    @Override
    public boolean equals(Object obj) {
        if (this == obj)
            return true;
        if (obj == null)
            return false;
        if (getClass() != obj.getClass())
            return false;
        MutableCustomKey other = (MutableCustomKey) obj;
        if (name == null) {
            if (other.name != null)
                return false;
        } else if (!name.equals(other.name))
            return false;
        return true;
    }

    public static void main(String[] args) {
        MutableCustomKey key = new MutableCustomKey("Shamik");
        Map<MutableCustomKey, String> map = new HashMap<MutableCustomKey, String>();
        map.put(key, "Shamik Mitra");
        MutableCustomKey refKey = new MutableCustomKey("Shamik");
        String val = map.get(refKey);
        System.out.println("Value Found " + val);
        key.setName("Bubun");
        String val1 = map.get(refKey);
        System.out.println("Due to MutableKey value not found " + val1);
    }
}
 

속성이 변경되면 프로그램에선 찾을 수 없지만, Map에서는 참조가 있으므로 메모리 누수가 발생.

 

# 6. 자료구조를 생성하여 사용하면서, 구현 오류로 인해 메모리를 해제하지 않는 경우

public class Stack {

       privateint maxSize;
       privateint[] stackArray;
       privateint pointer;
       
       public Stack(int s) {
              maxSize = s;
              stackArray = newint[maxSize];
              pointer = -1;
       }
       
       public void push(int j) {
              stackArray[++pointer] = j;
       }
       
       public int pop() {
              return stackArray[pointer--];
       }
       
       public int peek() {
              return stackArray[pointer];
       }
       
       publicboolean isEmpty() {
              return (pointer == -1);
       }
       
       public boolean isFull() {
              return (pointer == maxSize - 1);
       }
       
       public static void main(String[] args) {
       
              Stack stack = new Stack(1000);
              
              for(int i = 0; i<1000; i++) {
                     stack.push(i);
              }
              
              for(int i = 0; i<1000; i++) {
                     int element = stack.pop();
                     System.out.println("Poped element is "+ element);
              }
       }
}
Stack이 1000으로 커지면서 내부 배열인 stackArray도 값이 채워지게 된다. 그 후 Stack를 pop하면 Stack의 참조된 공간이 비어있지만, stackArray에는 pop된 모든 참조가 포함되게 된다. 자바에선 이를 쓸모없는 참조라 불린다. 혹은 구식 참조(역 참조 할 수 없는 참조)라고 불린다. 배열에 해당 요소가 포함되어 있으면 GC가 될 수 없지만, pop된 후 에는 불필요하다.

 

이 문제를 해결하려면 pop이 실행될 때, null 값을 설정하여 해당 객체가 GC가 되도록 해야한다. 

public int pop() {
              int size = pointer--
              int element= stackArray[size];
              stackArray[size];
              return element;
       }
 

메모리 누수가 계속 생겨 결국에 OOM이 발생한다면, OOM이 발생하는 영역들은 어떤 영역들이 있을까?
OOM 현상은  Young영역, Old 영역, Metaspace 영역 혹은 Native영역에서 모두 발생할수 있다. 각 영역별로 메모리릭이 나는 원인이 다르기에, 메모리릭을 찾는 일은 그리 쉽지 않은 작업일 수 있다. 

 

우선 본론을 말하기전 간단히

세대별 가비지 컬렉션을 간단히 말하자면,

 

1. 새로운 객체는 에덴(Eden) 공간에 할당되며, 그 외 두 개의 생존 공간이 모두 비어있는 상태이다.

2. 에덴 공간이 가득차게 되면 사소한(가벼운) 가비지 컬렉션이 시작돤다.

3. 참조된 객체는 첫번째 생존 공간으로 이동되며 참조되지 않는 객체는 모두 삭제된다.

4. 가비지 컬렉션이 수행되는 동안 첫번째 생존 공간의 객체들은 특정 임계값이 넘어가면 두번째 생존 공간으로 이동한 다.

5. 두 번째 생존 공간의 객체들도 특정 임계값이 넘어가면 old 영역으로 넘어가게 된다.

6. young 영역의 객체가 일정 크기 이상 수집되면 주요 가비지 컬렉션이 수행된다.

 

더 자세한건 여기

 
[Java] Garbage collection (1)

자바 프로그래머라면 Garbage collection은 꼭!꼭! 자세히 알아야 할 부분이다. 자바에서는 JVM이 구성되어진 JRE가 제공되며 JVM에 구성되어 있는 가비지컬렉션이 자동으로 사용하지 않는 객체를 파괴

junghyungil.tistory.com
를 참조해보면 된다.

 

1. young 영역
이때 객체의 크기가 Eden,S0,S1보다 크면 OOM가 발생할수 있다.

 

2. Old 영역
oung영역에서 오랫동안 GC되지 않고 살아남으면 Old영역으로 메모리가 이동하게 되는데, 만약 Old영역의 모든 객체가 여전히 강참조로 남아있고, 더이상 새로운 객체가 Young영역에서 이동해올 공간이 없다면 OOM 이 발생한다. JVM의 옵션으로  Young과 Old의 비율을 마음대로 조정할수가 있는데, 이러한 과정에서 비율 설정이 잘못될 경우 OOM으로 발전할 가능성도 존재한다.

 

3. Metaspace영역
메타스페이스 영역은 객체가 아닌 클래스의 정보가 로드되는 영역이다.

 

크기가 큰 많은 클래스가 로딩될 경우 metaspace로 OOM이 발생 할 수 도 있다. 이 영역에서 OOM은 일반적인 경우에서는 흔치 않다.

 

종종 Metaspace OOM은 bytecode weaving기술을 잘못 사용하는 경우에 많이 발생한다.  개발자들이 작성하는 대부분의 로직은 명시적인 new를 통해서 직접적으로 클래스를 로딩한다. 그런데 때로는 직접코드를 통해 클래스를 로딩하지 않아도 클래스가 로딩되는 경우가 있다. 스프링 MVC같은 웹프레임워크를 사용하는 경우 annotation이나 xml, 스크립트등으로 객체를 생성하는 경우들이 있다.  이런 경우에는 유저가 new를 호출하지 않았지만 클래스가 로딩되기도 한다. 자바에서는 이런 기술들을 weaving 방식이라고 하며, 디버깅이나 트랜잭션, 로깅들에서 다양하게 이용한다. 문제는 이런 weaving기술들이 편하기는 하지만 때로는 사용하는 라이브러리들이 버그를 가지고 있어, 클래스를 무제한으로 생성시키기도 한다는 점이다. 이런경우 OOM이 발생할수도 있다. 

 

4. native 영역
기본적으로 JVM은 자체 heap영역 / metaspace영역을 사용하지만,  실제 동작하면서 JNI나 Thread쪽은 OS의 메모리를 사용한다. 특히 쓰레드의 경우에는 OS의 쓰레드/스택메모리를 사용하기 때문에, new Thread()시에도 Native 메모리가 모자라면 OOM이 발생할수 있다. 그외에 NIO같은 native메모리를 바로 사용하는 경우에도 OOM이 발생할 수 있다.

 

 

메모리 릭을 방지하거나 해결하기 위해서 기본적으로 코드를 잘 짜는 것이 중요하겠지만, 서비스가 커졌을 경우를 고려해서 성능 테스트와 GC 옵션 튜닝에 관해 공부 해보아야 겠다.

https://junghyungil.tistory.com/133
