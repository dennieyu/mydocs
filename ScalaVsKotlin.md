Scala vs Kotlin
=====

Scala는 아카데미에서 설계되었으며, Kotlin은 선도적인 소프트웨어 회사에서 출발 했다. 그들이 태어난 배경이 그 차이점을 잘 설명 해 주고 있다. Scala는 함수형 프로그래밍과 다른 패러다임 간의 하이브리드라는 멋진 아이디어를 실현하기 위해 탄생했다. Kotlin은 실용적인 문제를 해결하고자 한다. Kotlin 디자이너는 컴파일 시간과 훌륭한 도구 지원에 특히 신경을 썼다.

**Kotlin은 "필요한" 모든 것을 제공하며, Scala는 "원하는" 모든 것을 제공한다.**


Kotlin
----

```
fun main() {
    val a = listOf("pop", "classic", "pop", "classic", "pop")

    println(
        a.indices
         .groupBy { a[it] }
         .toList()
         .map { it.second.sortedByDescending { it }.take(2) }
         .flatten()
    )
}
```

[**Playground**](https://play.kotlinlang.org/)


Scala
----

```
val a = List("pop", "classic", "pop", "classic", "pop")

println(
  a.indices
    .groupBy(x => a(x))
    .toList
    .map(x => x._2.sortBy(v => -v).take(2))
    .flatten
)
```

[**Playground**](https://scastie.scala-lang.org/)


Kotlin은 더 나은 Java인가?
-----
Kotlin은 원래 목표를 달성했다고 주장 할 수 있다. Java가 아닌 Android 개발을 위해 공식적으로 지원되는 첫 번째 언어가 되었다. 이는 Java 공동체가 Kotlin을 좋아하고 Java 개발자에게 Kotlin을 소개하는 것이 쉽다는 것을 입증하는 위대한 업적이다.

Kotlin은 생산성을 향상시키고 Java 개발자에게 배우기 쉽도록 만들어진 실용적인 언어이다. 주로 Java와 비슷하게 디자인 되었지만 Java 모델 위에서 C# 및 Scala 의 좋은 모습 또한 포함되어 있다. 람다 및 기본 기능과 같은 Java 프로그래머가 원하는 기능을 추가하고 스마트 캐스팅 및 null이 허용되지 않는 타입과 같은 것을 통해 개발자 생활을 단순화 시킨다. 


Scala는 Java보다 강력합니다.
-----
Scala는 그 일 (더 나은 Java) 를 시도하기 보다는 Java보다 강력하도록 설계되었다. 일반적으로 Java보다 더 나은 언어이다. Scala는 Java가 할 수없는 일을 하도록 설계되었다.

Scala는 고급 함수 프로그래밍을 훌륭하게 지원한다. 하지만 이로 인해 복잡성이 증가하고 배우고 사용하기 좀 어렵기로 언어로 만들 수 있다.

