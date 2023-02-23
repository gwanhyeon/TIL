
# Stack VS Heap 

자바에서 메모리라 함은 Stack 영역과 Heap 영역으로 나뉘어 진다.

Stack의 경우에는 정적으로 할당된 메모리 영역이다.

Stack에서는 Primitive 타입 (boolean, char, short, int, long, float, double) 의 데이터가 값이랑 같이할당이 되고,
또 Heap 영역에 생성된 Object 타입의 데이터의 참조 값이 할당 된다.

그리고 Stack 의 메모리는 Thread당 하나씩 할당 된다. 만약 새로운 스레드가 생성되면 해당 스레드에 대한 Stack이 새롭게 생성되고, 각 스레드 끼리는 Stack 영역을 접근할 수 가 없다.

Heap의 경우에는 동적으로 할당된 메모리 영역이다.

힙 영역에서는 모든 Object 타입의 데이터가 할당이 된다. (참고로 모든 객체는 Object 타입을 상속받는다.)
Heap 영역의 Object를 가리키는 참조변수가 Stack에 할당이 된다. 어플리케이션에서의 모든 메모리 중에서 Stack에 쌓이는 애들 빼고는 전부 이 Heap 쌓입니다.


추후 보완해서 올릴예정입니다.
