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



Distinctions﻿
Because the scope functions are all quite similar in nature, it's important to understand the differences between them. There are two main differences between each scope function:

The way to refer to the context object.

The return value.

Context object: this or it﻿
Inside the lambda of a scope function, the context object is available by a short reference instead of its actual name. Each scope function uses one of two ways to access the context object: as a lambda receiver (this) or as a lambda argument (it). Both provide the same capabilities, so we'll describe the pros and cons of each for different cases and provide recommendations on their use.
```kotlin
fun main() {
    val str = "Hello"
    // this
    str.run {
        println("The string's length: $length")
        //println("The string's length: ${this.length}") // does the same
    }
​
    // it
    str.let {
        println("The string's length is ${it.length}")
    }
}
```
# this﻿
run, with, and apply refer to the context object as a lambda receiver - by keyword this. Hence, in their lambdas, the object is available as it would be in ordinary class functions. In most cases, you can omit this when accessing the members of the receiver object, making the code shorter. On the other hand, if this is omitted, it can be hard to distinguish between the receiver members and external objects or functions. So, having the context object as a receiver (this) is recommended for lambdas that mainly operate on the object members: call its functions or assign properties.
```
val adam = Person("Adam").apply { 
    age = 20                       // same as this.age = 20 or adam.age = 20
    city = "London"
}
println(adam)
```

# it﻿
In turn, let and also have the context object as a lambda argument. If the argument name is not specified, the object is accessed by the implicit default name it. it is shorter than this and expressions with it are usually easier for reading. However, when calling the object functions or properties you don't have the object available implicitly like this. Hence, having the context object as it is better when the object is mostly used as an argument in function calls. it is also better if you use multiple variables in the code block.
```
fun getRandomInt(): Int {
    return Random.nextInt(100).also {
        writeToLog("getRandomInt() generated value $it")
    }
}
​
val i = getRandomInt()
println(i)
```

Additionally, when you pass the context object as an argument, you can provide a custom name for the context object inside the scope.
```
fun getRandomInt(): Int {
    return Random.nextInt(100).also { value ->
        writeToLog("getRandomInt() generated value $value")
    }
}
​
val i = getRandomInt()
println(i)
```
Return value﻿
The scope functions differ by the result they return:

apply and also return the context object.

let, run, and with return the lambda result.

These two options let you choose the proper function depending on what you do next in your code.

Context object﻿
The return value of apply and also is the context object itself. Hence, they can be included into call chains as side steps: you can continue chaining function calls on the same object after them.
```
val numberList = mutableListOf<Double>()
numberList.also { println("Populating the list") }
    .apply {
        add(2.71)
        add(3.14)
        add(1.0)
    }
    .also { println("Sorting the list") }
    .sort()
```

They also can be used in return statements of functions returning the context object.
```
fun getRandomInt(): Int {
    return Random.nextInt(100).also {
        writeToLog("getRandomInt() generated value $it")
    }
}
​```
val i = getRandomInt()
Open in Playground →
Target platform: JVM
Running on kotlin v.1.6.10
Lambda result﻿
let, run, and with return the lambda result. So, you can use them when assigning the result to a variable, chaining operations on the result, and so on.
```

```kotlin
val numbers = mutableListOf("one", "two", "three")
val countEndsWithE = numbers.run { 
    add("four")
    add("five")
    count { it.endsWith("e") }
}
println("There are $countEndsWithE elements that end with e.")
Open in Playground →
Target platform: JVM
Running on kotlin v.1.6.10
Additionally, you can ignore the return value and use a scope function to create a temporary scope for variables.
```

```kotlin
val numbers = mutableListOf("one", "two", "three")
with(numbers) {
    val firstItem = first()
    val lastItem = last()        
    println("First item: $firstItem, last item: $lastItem")
}
val numbers = mutableListOf("one", "two", "three")
with(numbers) {
    val firstItem = first()
    val lastItem = last()        
    println("First item: $firstItem, last item: $lastItem")
}
```
