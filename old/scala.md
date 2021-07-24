[**출처 - Programmers/프로그래밍 강의**](https://programmers.co.kr/learn/courses/12)

## 파트1. 변수와 계산 (4 / 4)

#### Hello, world!

설명
```
```

코드
```
object LearnScala {
    def main(args: Array[String]): Unit = {
        println("Hello, world!")
    }
}
```

#### 변수와 계산하기

설명
```
스칼라에서 1(Int 리터럴)과 같은 원시 타입(Primitive)은 객체(Object)로 취급됩니다. 그래서 +와 같은 연산자는 사실 (1)이라는 원시 타입 객체의 메소드인데요.
1 + 2라는 식은 1이라는 객체에 +라는 메소드를 호출하는 것이고 인자로 2가 전달되는 겁니다.

스칼라에서는 +-*/같은 수학 연산을 지원하기 위해 연산자 메소드들에는 우선순위를 매기고 있습니다. +와 *를 순서대로 호출하더라도 *가 먼저 수행되어야 하기 때문이지요.
이와 같은 표현 방식은 연산자 표기방식(Operator notation) 또는 infix 표기방식이라고 합니다.

스칼라의 원시 타입은 스칼라에서 객체로 취급되지만, 컴파일 이후에는 성능을 위해 자바의 원시 타입을 이용합니다.(자바의 원시 타입을 쓸 수 있는 경우에 만요)
```

코드
```
object LearnScala {
    def main(args: Array[String]): Unit = {
        println( 1 + 2 )
        println( 1.+(2) )
    }
}
```

#### 변수와 상수

설명
```
변수는 var로 상수는 val로 선언합니다.

한 번에 여러 개의 변수를 선언하고 값을 대입할 수도 있습니다.
```

코드
```
object LearnScala {
    def main(args: Array[String]): Unit = {
        var x = 1 + 2
        x = 3 * 4
        println( x )
        
        val y = 1 + 2
        // y = 3 * 4 // 이 줄은 상수에 값을 대입해서 에러가 나기 때문에 지워야 합니다.
        println( y )
        
        // 한 번에 여러개의 변수를 선언하면서 값을 대입할 수도 있습니다.
        var a, b, c = 5
        println( a )
        println( b )
        println( c )
    }
}
```

#### 변수 출력하기

설명
```
스칼라는 println, printf를 쓸 수 있습니다. 
```

코드
```
object LearnScala {
    def main(args: Array[String]): Unit = {
        var x = 10
        var y = 1
        
        // ① println
        println("① " + x + " is bigger than " + y)  
        
        // ② 문자열 앞에 s를 쓰면 $를 쓰고 변수이름을 바로 쓸 수 있습니다.
        println(s"② $x is bigger than $y")
        
        // ③ 수식을 입력하고 싶으면 ${ }사이에 식을 넣으면 됩니다.
        println(s"③ $x + $y = ${ x + y }")
        
        // ④ printf도 사용 가능합니다.
        //java.lang.*은 자동으로 import됩니다.
        //java.lang.Math도 포함입니다.
        printf("④ Pi is %f", Math.PI)
    }
}
```

## 파트2. 편리한 스칼라 (3 / 3)

#### Range와 List

설명
```
스칼라는 Range와 List를 생성하고 다루는 유용한 도구들을 제공합니다. 
```

코드
```
object LearnScala {
    def main(args: Array[String]): Unit = {
        // ① to를 이용하면 1부터 10을 포함하는 Range를 생성합니다.
        val range1 = 1 to 10
        println(s"① 1 to 10 →\n\t $range1")
        
        // ② until을 이용하면 마지막 숫자를 포함하지 않는 Range를 생성합니다.    
        val range2 = 1 until 10
        println(s"② 1 until 10 →\n\t $range2")
        
        // ③ by를 이용하면 숫자를 건너 띄는 Range를 생성합니다.
        val range3 = 1 until 10 by 3
        println(s"③ 1 until 10 by 3 →\n\t $range3")
        
        // ④ toList를 통해 List로 변환합니다.
        println(s"④ range1.toList →\n\t ${range1.toList}")
        
        // ⑤ filter: 조건에 맞는것만 모으기(4 이상인것만 모으기)
        val moreThan4 = range1.filter(_ > 4)  
        println(s"⑤ range1.filter(_ > 4) →\n\t $moreThan4")
        
        // ⑥ map - 각 아이템의 값을 변경하기
        val doubleIt = range1.map(_ * 2)  
        println(s"⑥ range1.map(_ * 2) →\n\t $doubleIt")
    }
}
```

#### 숫자 다루기

설명
```
스칼라에서 숫자를 쉽게 다룰 수 있도록 도와주는 메소드를 사용해 보세요. 
```

코드
```
object LearnScala {
    def main(args: Array[String]): Unit = {
        val num = -5  
        val numAbs = num.abs // 절대값
        val max5or7 = numAbs.max(7) // 5(numAbs)와 7 사이의 최대값  
        val min5or7 = numAbs.min(7) // 5(numAbs)와 7 사이의 최소값
        println(numAbs) // 5  
        println(max5or7) // 7   
        println(min5or7) // 5  
    }
}
```

#### 문자열 다루기

설명
```
문자열을 쉽게 다룰 수 있도록 도와주는 스칼라의 도구들입니다.
```

코드
```
object LearnScala {
    def main(args: Array[String]): Unit = {
        // ① 뒤집기
        val reverse = "Scala".reverse 
        println(s"① $reverse")
        
        // ② 첫글자를 대문자로
        val cap = "scala".capitalize
        println(s"② $cap")
        
        // ③ 7번 반복
        val multi = "Scala! " * 7
        println(s"③ $multi") 
        
        // ④ 정수로 변환
        val int = "123".toInt
        println(s"④ $int")
    }
}
```

## 파트3. 메소드와 함수 (3 / 3)

#### 메소드 정의

설명
```
스칼라에서 메소드는 다양한 형태로 정의할 수 있습니다.
우선 리턴 값이 있는 메소드는 메소드를 정의하는 블록 { }전에 =을 적어주어야 합니다.
그리고 리턴 키워드는 옵션입니다. 적어주지 않으면 리턴 타입은 리턴 값에 의해 결정됩니다.
```

코드
```
object LearnScala {
    // ① 일반적인 메소드
    def add(x:Int, y:Int):Int = {
        return x + y        
    }
    
    // ② return을 생략한 메소드
    def addWithoutReturn(x:Int, y:Int) = { // x + y는 int이므로 return타입은 Int로 결정됩니다.
        x + y // return을 적어주지 않아도 마지막 값이 return값입니다.
    }
    
    // ③ 메소드가 한 줄일 경우 중괄호{}를 생략해도 됩니다.
    def addWithoutBlock(x:Int, y:Int) = x + y
    
    def main(args: Array[String]): Unit = {
        println(s"① ${add(1,2)}")
        println(s"② ${addWithoutReturn(1,2)}")
        println(s"③ ${addWithoutBlock(1,2)}")          
    }
}
```

#### 익명함수1

설명
```
스칼라에서 익명 함수(Anonymous Function)는 다음과 같은 형태로 정의합니다.

// 이 함수의 타입은 하나의 Int형 매개변수를 받아 Int형으로 그 제곱을 리턴하는 Int => Int입니다.
(x: Int) => x * x

// 이 함수의 타입은 두 개의 Int형 매개변수를 받아 그 합을 Int를 리턴하는 (Int, Int) => Int입니다.
(x: Int, y: Int) => x + y

익명 함수는 타입을 가지는데요. 예를 들어 다음 코드의 doWithOneAndTwo를 보면 (Int, Int) => (Int)와 같은 타입의 익명 함수만 받아들입니다.
따라서 코드 13번째 줄과 같이 (x, y) => x + y와 같은 익명 함수를 매개변수로 사용할 수 있습니다.
여기서 x와 y의 타입을 지정하지 않고 생략했는데요. 컴파일러가 코드 4번째 줄을 보고 타입을 알 수 있기 때문입니다.

추가로 더 짧게 변수명을 생략할 수도 있습니다. x와 y가 익명 함수의 Body에서 딱 한 번만 사용된다면 _로 대체할 수 있는데요. 익명 함수의 Body에 나타나는 _의 순서는 매개변수에 정의된 순서대로 입니다.
예를 들어 _ / _는 x/y와 같습니다.

하지만 만약 y/x처럼 순서를 바꿔서 표현하고 싶으면 까다로워지는데요. (1/_)*_라고 표현해야겠지요. (1/x)*y는 y/x이니까요.
```

코드
```
object LearnScala {
    
    // 매개변수로 받은 익명함수에 1과 2를 넣어서 실행하는 메소드
    def doWithOneAndTwo(f: (Int, Int) => Int) = {  
        f(1, 2) //return은 생략되었지만, f(1, 2)의 결과가 return
    }
    
    def main(args: Array[String]): Unit = {
        // ① 명시적으로 타입을 선언하는 익명함수
        val call1 = doWithOneAndTwo((x: Int, y: Int) => x + y)
        
        // ② 코드4번째 줄에서 익명함수의 매개변수 타입(Int, Int)을 이미 정했기 때문에 생략
        val call2 = doWithOneAndTwo((x, y) => x + y)  
        
        // ③ 이렇게 요약할 수도 있음
        val call3 = doWithOneAndTwo(_ + _) // 매개변수의 순서대로 _에 대입됨
        
        println(call1, call2, call3)
    }
}
```

#### 익명함수2

설명
```
add1은 메소드 정의 강의에서 살펴본 대로 메소드가 한 줄일 경우 중괄호를 생략한 형태입니다.
add2는 익명 함수를 상수 add2에 저장하고 있습니다.
add3은 _를 이용했는데요. 첫 번째 _자리에 첫 번째 매개변수가 대입되고, 두 번째 _자리에 두 번째 매개변수가 대입됩니다.
add4와 같이 표현할 수도 있지만 자주 사용하는 방법은 아닙니다.

_를 이용한 함수의 표기 방식은 익명 함수를 고계 함수(Higher order function)에 매개변수로 전달하는 경우에 유용하게 사용할 수 있습니다.
```

코드
```
object LearnScala {    
    // ① 메소드를 정의하는 방식
    def add1(x:Int, y:Int) = x + y 
    
    // ② 익명함수
    val add2 = (x:Int, y:Int) => x + y 
    
    // ③ 익명함수를 정의하는 다른 방식
    val add3:(Int,Int)=>Int = _ + _ 
    
    // ④ 익명함수를 정의하는 또다른 방식(잘 사용 안함)
    val add4 = (_ + _):(Int,Int)=>Int 
    
    def main(args: Array[String]): Unit = {
        // 모두 두 숫자를 더해주는 역할을 하므로 같은 결과를 출력
        println(s"① ${add1(42,13)}")  
        println(s"② ${add2(42,13)}")  
        println(s"③ ${add3(42,13)}")  
        println(s"④ ${add4(42,13)}")  
    }
}
```

## 파트4. 튜플 (3 / 3)

#### 튜플

설명
```

```

코드
```

```

#### 여러개의 값 리턴

설명
```

```

코드
```

```

#### 변수에 값 넣기

설명
```

```

코드
```

```

## 파트5. 제어문 (3 / 3)

#### 반복문

설명
```

```

코드
```

```

#### 중첩된 for문

설명
```

```

코드
```

```

#### if문

설명
```

```

코드
```

```

## 파트6. Collection (7 / 7)

#### Array

설명
```

```

코드
```

```

#### List

설명
```

```

코드
```

```

#### Set

설명
```

```

코드
```

```

#### Map

설명
```

```

코드
```

```

#### Array/List/Set/Map의 타입

설명
```

```

코드
```

```

#### 변경할 수 있는(Mutable) Collection

설명
```

```

코드
```

```

#### 변경할 수 없는(immutable) collection에서 var와 val사용

설명
```

```

코드
```

```

## 파트7. 클래스 (2 / 2)

#### 클래스

설명
```

```

코드
```

```

#### getter와 setter

설명
```

```

코드
```

```
