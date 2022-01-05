# Javascript


## Primitive type VS Reference type

**Primitive type** 
- Boolean
- number
- String
- null
- undefined
원시 타입의 데이터는 변수에 할당이 될 때 메모리 상에 고정된 크기로 저장이 되고 해당 변수가 원시 데이터 값을 보관한다. 
원시 타입 자료형은 모두 변수 선언, 초기화, 할당 시 값이 저장된 메모리 영역에 직접적으로 접근한다. 
즉, 변수에 새 값이 할당이 될 경우, 변수에 할당된 메모리 블럭에 저장된 값을 바로 변경한다.

```sql
const a = 3100;
let b = a;
b = 3;
console.log(a);
```

참조 없이 값이 변동 되었을때 메모리에 값을 그대로 저장한다.

**reference type**
참조 타입의 데이터는 크기가 정해져 있지 않고 변수에 할당이 될 때 값이 직접 해당 변수에 저장될 수 없으며 변수에는 데이터에 대한 참조만 저장된다.
 변수의 값이 저장된 힙 메모리의 주소값을 저장한다. 참조 타입은 변수의 값이 저장된 메모리 블럭의 주소를 가지고 있고 자바스크립트 엔진이 변수가 가지고 있는 메모리 주소를 이용해서 변수의 값에 접근한다.

 
- Object ( array, function, object )

$.extend({}, {}) Reference 타입으로 작성된 값들(객체, 배열, 함수 → Object) 타입

```sql
const origin = {
    key : 'a'
}

const originTemp = origin;
originTemp.b = 1000;
console.log(origin.b);
```

copy 라는 변수에 할당된것은 origin의 메모리 주소이며, 그로 인해 copy의 값을 바꿨지만 사실은 origin 메모리 주소에 들어가있는값을 바꾼것이므로 origin 값도 변경된다 
