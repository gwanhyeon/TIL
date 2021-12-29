# Kotlin Standard library
[코틀린 공식 문서](https://kotlinlang.org/docs/scope-functions.html)

## Scope functions

The Kotlin standard library contains several functions whose sole purpose is to execute a block of code within the context of an object. When you call such a function on an object with a lambda expression provided, it forms a temporary scope. In this scope, you can access the object without its name. Such functions are called scope functions. There are five of them: `let, run, with, apply, and also.`

객체 컨텍스트 내에서 코드 블록을 실행하면 함수를 호출시에 임시 범위가 형성되어 접근하여 처리 할 수 있습니다. 이것을 `scope function` 이라 부릅니다. scope function의 종류는 기본적으로 let, run, with, apply, also 가 존재합니다.

```kotlin

# scope function

Person("Alice", 20, "Amsterdam").let {
    println(it)
    it.moveTo("London")
    it.incrementAge()
    println(it)
}
Person(name=Alice, age=20, city=Amsterdam)
Person(name=Alice, age=21, city=London)

# It's not a scope function 

val alice = Person("Alice", 20, "Amsterdam")
println(alice)
alice.moveTo("London")
alice.incrementAge()
println(alice)
```

스코프 함수를 사용하여 객체 컨텍스트내에서 처리하는것과 직접적으로 처리하는것과의 차이점이 확연하게 보입니다. 스코프 함수는 코드를 간결하게 만들 수 있고 이것은 프로젝트의 의도성과 일관성에 따라 달라집니다. 

### scope function - Function selection 

- Executing a lambda on non-null objects: `let`
null의 객체가 아닐 경우 

- Introducing an expression as a variable in local scope: `let`
로컬 변수로 사용

- Object configuration: `apply`
객체의 설정 

- Object configuration and computing the result: `run`
객체의 설정 및 결과 처리

- Running statements where an expression is required: `non-extension run`
비확장 실행 처리 

- Additional effects: `also`
추가적인 기능 처리 

- Grouping function calls on an object: `with`
함수간의 그룹핑 처리 
