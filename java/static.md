# Java Static(정적 메소드)

`static variable / static method / static class ....`

static 키워드가 붙으면 JVM이 시작될 때 Method(static) 영역에 저장된다. 그리고 프로그램이 끝날 때 까지 사라지지 않고 메모리에 남아 있다.

> static method

속도가 빨라지고 공유(반복적인 사용)에 효율적이다. 

```java
public class LottoNumberFactory {

    private static final int MIN_LOTTO_NUMBER = 1;
    private static final int MAX_LOTTO_NUMBER = 45;
    private static final int LOTTO_LENGTH = 6;

    private static List<LottoNumber> lottoNumbers = new ArrayList<>();

    //45개의 로또 숫자 초기화
    static {
        for (int i = MIN_LOTTO_NUMBER; i <= MAX_LOTTO_NUMBER; i++) {
            lottoNumbers.add(new LottoNumber(i));
        }
    }

    public static List<LottoNumber> createLottoNumbers() {
        List<LottoNumber> lotto = new ArrayList<>();
        Collections.shuffle(lottoNumbers);
        for (int i = 0; i < LOTTO_LENGTH; i++) {
            lotto.add(lottoNumbers.get(i));
        }
        return lotto;
    }

}

```

static으로 선언 되어 있을 때 메소드를 사용할 때 마다 반복적으로 LottoNumberFactory 객체를 생성해 줄 필요가 없다. 생성자를 호출 할 필요가 없으니 당연히 속도가 빨라질 수 밖에 없다.

> static 사용이 그래서 올바른 것일까?

- 객체지향에서 멀어진다
- 메모리 효율이 떨어질 수 있다.
- static 키워드는 C의 전역변수/함수와 성격이 비슷하다. 정적 메소드는 객체의 생성, 제거와 관계없이 프로그램 시작부터 끝날 때까지 메모리에 남아 있다.

> Polymorphism(다형성)

- 정적 메소드는 객체의 생성주기와 관계가 없다.
- 정적 메소드는 객체 지향의 메시지 전달(message passing)을 위반한다.
- 결과적으로, 절차지향적인 부분과 유사하다.

> Overriding / Dynamic Binding

```java
public abstract class WoowaTechCrew {
    public void hello() {
        System.out.println("안녕하세요.");
    }
}

public class Orange extends WoowaTechCrew {
    @Override
    public void hello() {
        System.out.println("하이요!");
    }
}

public class Kafka extends WoowaTechCrew {
    @Override
    public void hello() {
        System.out.println("안녕하쎄요~");
    }
}

// main
public static void main(String[] args) {
    WoowaTechCrew orange = new Orange();
    WoowaTechCrew kafka = new Kafka();
    orange.hello();
    kafka.hello();
}
```

- 다형성은 같은 타입으로 묶을 수 있는 여러 객체에게 동일한 명령을 내리면 각 객체에 맞는 다른일을 수행한다.
- 하지만, 정적 메소드는 객체지향의 다형성을 위반한다.
- 정적메소드는 런타임 이전 컴파일 시에 정적 바인딩이 이루어진다.
- 메모리 효율이 떨어질 수도 있는데, 런타임 중 동적으로 생성 된 것들은 GC(Garbage Collection)의 대상이 되는 반면, static 키워드가 붙은 메소드 등은 GC의 대상이 아니다. GC는 동적으로 할당된 메모리만을 대상으로 한다. 따라서, static 영역은 GC의 대상이 아니다.

> 추가

- 2. 메모리 효율이 떨어질 수 있다. 에서 메서드는 static 키워드가 붙든 말든 컴파일 과정에서 Metaspace(자바 8 아래 버전에선 Permgen)에 담긴다고 한다.

> reference

https://tecoble.techcourse.co.kr/post/2020-07-16-static-method/
