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
t1과 같이 튜플은 여러 타입의 객체를 담을 수 있습니다.
t1을 줄여서 t2와 같이 많이 사용합니다

튜플은 내부적으로 담고 있는 객체의 수에 따라 다른 클래스로 구현되는데요. t1과 같이 3개의 객체를 담고 있으면 Tuple3 클래스를 이용하게 됩니다. 
Tuple1부터 Tuple22까지 사용할 수 있고 그 이상을 쓰려면 컬렉션과 같은 다른 자료구조를 사용해야 합니다.

튜플의 값에 접근하려면 ._1, ._2와 같은 메소드를 사용하면 됩니다.
```

코드
```
object LearnScala {
    def main(args: Array[String]): Unit = {
        val t1 = new Tuple3(1, "hello", true)
        val t2 = (1, "hello", true)
        
        println(t2)
        
        var numbers = (1,2,3,4)
        val sum = numbers._1 + numbers._2 + numbers._3 + numbers._4
        println(sum)
    }
}
```

#### 여러개의 값 리턴

설명
```
튜플을 이용해서 한 번에 여러 개의 값을 리턴할 수 있습니다.
```

코드
```
object LearnScala {
    def swap(x:String, y:String) = (y, x)  
    
    def main(args: Array[String]): Unit = {
        val (a,b) = swap("hello","world")
        println(a, b)
    }
}
```

#### 변수에 값 넣기

설명
```
튜플을 이용해서 한 번에 여러 개의 변수에 값을 넣을 수 있습니다. 
```

코드
```
object LearnScala {
    def main(args: Array[String]): Unit = {
        var (x, y, z, c, python, java) = (1, 2, 3, true, false, "no!")  
        println(x, y, z, c, python, java)
    }
}
```

## 파트5. 제어문 (3 / 3)

#### 반복문

설명
```
스칼라는 while문, for문을 제공합니다.
++나 --는 제공하지 않으므로 += 1을 사용해야 합니다.

하지만 합을 구하는 가장 스칼라스러운 방법은 코드의 19번째 줄에 있는 방법입니다.
스칼라에서는 while문을 사용하는 대신에 이런 방법으로 대체할 수 있는 경우가 많습니다.
```

코드
```
object LearnScala {
    def main(args: Array[String]): Unit = {
        // ① while문
        var i, sum = 0  
        while ( i < 10) {  
            sum += i  
            i+=1 
        }  
        println(s"① $sum")
        
        // ② for문
        sum = 0  
        for ( i <- 0 until 10) {  
            sum += i  
        }  
        println(s"② $sum")  
        
        //③ 가장 스칼라스럽게 합을 구하는 방법
        sum = (0 until 10).sum  
        println(s"③ $sum")
    }
}
```

#### 중첩된 for문

설명
```
for문에 여러 개의 range를 세미콜론으로 구분해서 적어주면 for문을 중첩해서 사용한 것과 같은 효과입니다.
```

코드
```
object LearnScala {
    def main(args: Array[String]): Unit = {
        for( a<- 1 to 3) {
            for( b <- 10 to 12) {
                println(a,b)
            }
        }
        println("중첩된 for문 대신 아래와 같이 쓸 수 있습니다.")
        for( a <- 1 to 3; b <- 10 to 12) {
            println(a,b)
        }
    }
}
```

#### if문

설명
```
조건문은 Java나 C와 거의 같습니다.

하지만 스칼라에서 중요한 차이점은 if문도 수식(Expression)이라는 점입니다.
그래서 코드의 16번째 줄과 같이 if문만으로 삼항 연산자를 대신할 수 있습니다.
```

코드
```
object LearnScala {
    def main(args: Array[String]): Unit = {
        if (true)   
            println("한 줄은 {괄호}를 생략할 수 있습니다.")  
        
        if (1 + 1 == 2) {  
            println("여러 줄은")  
            println("{괄호}가 필요합니다.")  
        } else {  
            println("컴퓨터가 미쳤나봐요.")  
        }
        
        val likeEggs = false  
        // 삼항 연산자대신 이렇게 쓸 수 있습니다.
        val breakfast =  
          if (likeEggs) "계란후라이"  
          else "사과"  
        
        println(s"아침으로 ${breakfast}를 먹어요")  
    }
}
```

## 파트6. Collection (7 / 7)

#### Array

설명
```
배열은 Array(element1, element2, ...)와 같이 만들 수 있습니다.

스칼라의 배열은 자바의 배열에 대응하는 개념입니다. 예를 들어 자바에서 int[]는 스칼라에서 Array[Int]와 같습니다.

스칼라의 배열은 mutable입니다. 사이즈를 변경할 수 있다는 의미가 아니라 들어있는 값을 변경할 수 있다는 의미의 mutable입니다.

배열은 그냥 출력하면 배열의 내용을 출력해 주지 않습니다. 내용을 출력하려면 .mkString(",")과 같은 메소드를 이용해야 합니다.
```

코드
```
object LearnScala {
    // 배열의 내용을 출력하는 메소드
    def printArray[K](array:Array[K]) = println(array.mkString("Array(" , ", " , ")")) 
    def main(args: Array[String]): Unit = {
        
        // ① Array[Int]  
        val array1 = Array(1, 2, 3)
        print("① ")
        printArray(array1)
        
        // ② Array[Any]
        val array2 = Array("a", 2, true)
        print("② ")
        printArray(array2)
        
        // ③ 배열의 값을 읽고 쓰기
        val itemAtIndex0 = array1(0)        
        array1(0) = 4
        print("③ ")
        printArray(array1)
        
        // ④ 배열을 붙일때는 ++연산자를 이용
        // 앞에 붙일때는 +:, 뒤에 붙일때는 :+ 연산자
        val concatenated = "앞에 붙이기" +: (array1 ++ array2) :+ "뒤에 붙이기"
        print("④ array1과 array2를 더하면: ")
        printArray(concatenated)
        
        // 값으로 index찾기
        array2.indexOf("a")
        
        // ⑤ 다른 값만 가져오기
        val diffArray = Array(1,2,3,4).diff(Array(2,3))
        print("⑤ Array(1,2,3,4).diff(Array(2,3))의 결과: ")
        printArray(diffArray)
        
        
        val personArray = Array(("솔라",1), ("문별",2), ("휘인",3))        
        // ⑥ Find 메소드를 이용해서 findByName이라는 메소드 생성
        // Find는 조건에 맞는 값을 찾으면 검색을 중단
        // getOrElse는 일치하는 값이 없을 경우 넘겨줄 기본 값
        // getOrElse가 없을때 일치하는 값이 없으면 None
        def findByName(name:String) = personArray.find(_._1 == name).getOrElse(("화사",4))
        val findSolar = findByName("솔라")  // 값("솔라",1)을 찾아서 넘겨줌
        val findSun = findByName("태양")  // 값이 없으므로 getOrElse에 있는 값("화사",4)이 들어감
        println(findSolar)
        println(findSun)
    }
}
```

#### List

설명
```
리스트는 List(element1, element2, ...)와 같이 생성합니다.

스칼라의 기본 List는 scala.collection.immutable.List이므로 값을 변경할 수 없는 속성을 가지고 있습니다. 
즉, 리스트에 값을 추가하거나 제거하는 작업은 원래 리스트에 반영되는 게 아닙니다. 해당 변경사항을 반영한 새로운 리스트를 만들어내는 방식으로 동작합니다.

기본 List는 Linked list로 구현됩니다.
```

코드
```
object LearnScala {
    def main(args: Array[String]): Unit = {
        // List[Any](기본 리스트를 사용하므로 Immutable) 
        val list = List("a", 1, true)
        
        // ① 값을 읽어올 수는 있지만
        val firstItem = list(0)
        // 아래줄과 같이 값을 변경할 수는 없음
        // list(0) = "b"
        println(s"① $firstItem")
        
        // ② 앞에 붙이기는 :: 또는 +: 연산자
        // 리스트 두개를 붙이기는 ++ 또는 :::연산자
        // 뒤에 붙이기는 :+연산자(immutable list에서 효율적인 방법이 아님)
        val concatenated = 0 :: list ++ list :+ 1000
        println(s"② $concatenated")
        
        // ③ Diff
        val diffList = List(1,2,3,4) diff List(2,3)
        println(s"③ $diffList")
        
        //④ 배열의 Find와 같은 방식으로 동작
        val personList = List(("솔라",1), ("문별",2), ("휘인",3))
        def findByName(name:String) = personList.find(_._1 == name).getOrElse(("화사",4))
        val findSolar = findByName("솔라")  //값("솔라",1)을 찾아서 넘겨줌
        val findSun = findByName("태양")  //값이 없으므로 getOrElse에 있는 값("화사",4)이 들어감
        
        println(s"④ ${findSolar}, ${findSun}")
    }
}
```

#### Set

설명
```
Set은 Set(element1, element2, ...)와 같이 생성합니다.

스칼라에서 기본 Set은 Predef.Set입니다.

Set은 크기가 4일 때까지는 크기에 따라 별도 클래스가 있습니다. Set1, Set2, Set3, Set4인데요. 구성요소가 4개보다 많아지면 HashSet으로 구현됩니다.

Set은 집합에 대응하는 개념으로 같은 값을 추가하면 기존 값을 덮어쓰게 되고, 순서가 보장되지 않습니다.
```

코드
```
object LearnScala {
    def main(args: Array[String]): Unit = {
        // ① 내용을 수정할 수 없는 Set
        val set1 = Set("one", 1) 
        val set2 = Set(1,2,2,2,3,3,3) // 중복이 제거되고 Set(1, 2, 3)이 됨
        println(s"① $set2")
        
        // ② 값이 있는지 체크하는 방법은 괄호 안에 값을 넣어서 사용
        val oneExists = set2(1)  
        val fourExists = set2(4)  
        println(s"② oneExists: ${oneExists}, fourExists: ${fourExists}")
        
        // ③ set을 더하면 중복된 내용은 제거된 새로운 Set이 생성
        val concatenated = set1 ++ set2  
        println(s"③ $concatenated")
        
        // ④ Diff
        val diffSet = Set(1,2,3,4) diff Set(2,3)  
        println(s"④ ${diffSet}")
        
        
        /* ⑤ set.find 메소드를 이용해서 findByName이라는 메소드 생성
         * find는 조건에 맞는 값을 찾으면 검색을 중단
         * getOrElse는 일치하는 값이 없을 경우 넘겨줄 기본 값
         * getOrElse가 없을때 일치하는 값이 없으면 None
         */
        val personSet = Set(("솔라",1), ("문별",2), ("    휘인",3))  
        def findByName(name:String) = personSet.find(_._1 == name).getOrElse(("화사",4))  
        val findSolar = findByName("솔라")  // 값("솔라",1)을 찾아서 넘겨줌
        val findSun = findByName("태양")  //값이 없으므로 getOrElse에 있는 값("화사",4)이 들어감
        
        println(s"⑤ ${findSolar._2}, ${findSun._2}")
    }
}
```

#### Map

설명
```
Map은 Map(key1 -> value1, key2 -> value2, ...)와 같이 생성합니다.

스칼라에서 기본 Map은 Predef.Map(scala.collection.immutable.Map)입니다.

Map도 Set과 마찬가지로 구성요소가 4개일 때까지는 Map1, Map2, Map3, Map4라는 별도 클래스로 구현되지만 더 많아지면 HashMap으로 구현됩니다.

키는 중복할 수 없으며 Set와 마찬가지로 순서가 보장되지 않습니다.
```

코드
```
object LearnScala {
    def main(args: Array[String]): Unit = {
        // ① Map[String, Int] 타입의 맵 
        val map1 = Map("one" -> 1, "two" -> 2, "three" -> 3)   
        // Map[Any, Any] 타입의 맵
        val map2 = Map(1 -> "one", "2" -> 2.0, "three" -> false)   
        println(s"① $map1")
        
        // ② 중복된 키가 있으면 마지막 값을 사용
        println(s"② ${Map('a' -> 1, 'a' -> 2)}")
        
        // ③ key를 가지고 값을 읽어오기
        val one = map1("one")  
        println(s"③ ${one}")
        
        /* ④ 키가 없으면 NoSuchElementException이 발생
         * 예를들어 이런 경우> val fourExists = map1("four")   
         * get메소드를 이용해서 얻어오는 객체의 isDefine값으로 Key가 있는지 확인 가능*/
        val fourExistsOption = map1.get("four")  
        println(s"④ ${fourExistsOption.isDefined}")
        
        // ⑤ ++연산자로 두개의 Map을 더할 수 있으며, 중복된 키("three")의 값은 마지막 값으로 결정
        val concatenated = map1 ++ map2
        println(s"⑤ ${concatenated}")   
        
        // ⑥ find (List, Set과 같은 형태)
        val personMap = Map(("솔라",1), ("문별",2), ("휘인",3))  
        def findByName(name:String) = personMap.getOrElse(name, 4)  
        val findSolar = findByName("솔라")  // 값 1을 찾아서 넘겨줌
        val findSun = findByName("태양")  // 값이 없으므로 4를 넘겨줌
        println(s"⑥ ${findSolar}, ${findSun}")
    }
}
```

#### Array/List/Set/Map의 타입

설명
```
Array, List, Set, Map의 구성요소는 어떤 타입이든 사용할 수 있지만, 최종 타입은 공통으로 상속받는 타입 중 최상위 타입으로 결정됩니다.
```

코드
```
object LearnScala {
    class Animal()
    class Dog() extends Animal()
    
    def main(args: Array[String]): Unit = {
        // Animal과 Dog이 공통으로 상속받는 최상위 타입은 Animal이므로 아래 코드는 정상 실행
        val array:Array[Animal] = Array(new Animal(), new Dog())
        // val wrongArray:Array[Dog] = Array(new Animal(), new Dog()) 올바르지 않은 타입
        
        // List도 같은 원리로 동작(Animal이 List의 element의 타입)
        val list:List[Animal] = List(new Animal(), new Dog())
        
        // Set도 같은 원리로 동작(Animal이 Set의 element의 타입)
        val set:Set[Animal] = Set(new Animal(), new Dog())
        
        // Map도 같은 원리로 동작
        val map:Map[String, Animal] = Map("Animal" -> new Animal(), "Dog" -> new Dog())        
    }
}
```

#### 변경할 수 있는(Mutable) Collection

설명
```
스칼라는 변경할 수 없는(immutable) Collection을 사용하는 것을 권장합니다. 그래서 기본 Collection이 immutable입니다.

하지만 꼭 필요할 경우 변경할 수 있는(mutable) collection을 사용할 수 있습니다.

ArrayBuffer는 자바에서 배열로 구현되는 java.util.ArrayList와 유사합니다.

ListBuffer는 List처럼 Linked List로 구현됩니다.

mutable Collection을 사용할 때는 앞에 mutable을 붙여서 사용해 주세요.
(mutable.ArrayBuffer, mutable.ListBuffer, mutable.Set, mutable.Map)
```

코드
```
import scala.collection.mutable  

object LearnScala {
    def main(args: Array[String]): Unit = {        
        // ① 배열로 구현되는 ArrayBuffer
        val arrayBuffer = mutable.ArrayBuffer(1, 2, 3)   
        arrayBuffer += 4
        arrayBuffer -= 1  
        arrayBuffer ++= List(5, 6, 7)
        println(s"① $arrayBuffer")
        
        // ② Linked list로 구현되는 ListBuffer
        val listBuffer = mutable.ListBuffer("a", "b", "c")  
        println(s"② $listBuffer")
        
        // ③ Mutable Set
        val hashSet = mutable.Set(0.1, 0.2, 0.3)  
        hashSet ++= mutable.Set(5)
        println(s"③ $hashSet")
        
        // ④ Mutable Map
        val hashMap = mutable.Map("one" -> 1, "two" -> 2)  
        hashMap ++= Map("five" -> 5, "six" -> 6)
        println(s"④ $hashMap")
    }
}
```

#### 변경할 수 없는(immutable) collection에서 var와 val사용

설명
```
변경할 수 없는(immutable) Collection이 var로 선언된 경우에 Collection에 +=연산자나 -+연산자를 사용할 수 있습니다.
하지만 Collection 자체가 변경할 수 없는 형태이므로 이때는 변경사항을 반영한 새로운 Collection이 만들어져서 var로 선언된 변수에 저장됩니다.

변경할 수 있는(mutable) Collection의 경우에는 +=나 -=연산자가 collection의 메소드로 동작합니다.
```

코드
```
import scala.collection.mutable  

object LearnScala {
    def main(args: Array[String]): Unit = {        
        // ① 변경할 수 없는 Collection이 var로 선언된 경우
        var immutableSet = Set(1, 2, 3)   
        immutableSet += 4   
        // 위의 코드는 새로운 Set을 만들어서 immutableSet에 저장하는 아래 코드와 같음
        immutableSet = immutableSet + 4  
        println(s"① $immutableSet")
        
        // ② 변경할 수 있는 Collection이라면 추가하는 Method를 호출하는것과 같음
        val mutableSet = mutable.Set(1, 2, 3)    
        mutableSet += 4   
        // 위의 코드는 mutableSet 자체의 메소드(+=이라는 메소드)를 호출하는 아래 코드와 같음
        mutableSet.+=(4)  
        println(s"② $mutableSet")  
    }
}
```

## 파트7. 클래스 (2 / 2)

#### 클래스

설명
```
스칼라에서는 클래스를 아주 짧은 코드로도 만들 수 있는데요. 클래스를 선언하는 부분이 기본 생성자(constructor)의 역할도 하게 됩니다.

Person1.scala파일을 보세요. 이렇게 기본 생성자에 매개변수를 넣으면 fname과 lname이라는 이름을 가지는 private 변수가 생깁니다.

Person2.scala에서는 메소드를 정의하는 방법을 확인할 수 있습니다.

Person3.scala에서는 필드를 선언하는 방법을 확인할 수 있습니다.

Person4.scala처럼 매개변수를 val로 선언하면 해당 이름을 가지는 변수(private)와 public getter메소드를 생성합니다.
또 var로 생성자의 매개변수를 선언하면 해당 이름을 가지는 변수(private)와 public getter, setter메소드를 생성합니다.
를 확인하세요.

스칼라에서는 명시적으로 정의되지 않으면 모두 public으로 간주합니다.

주의
private 변수의 이름과 getter, setter가 모두 같은 이름을 가지는 경우를 직접 코드로 구현할 수는 없습니다.
getter와 setter를 사용하기 위해서는 private 변수의 이름은 다르게 지정해야 하는데요. 메소드명과 구분하기 위해 _를 변수명 앞에 붙이기도 합니다.
```

코드
```
object LearnScala {
    def main(args: Array[String]): Unit = {        
        // ① 단순한 클래스
        val p1 = new Person1("중기", "송")
        //p1.fname과 p1.lname의 값을 외부에서 가져올 수 없습니다.        
        
        // ② 메소드를 가지는 클래스
        val p2 = new Person2("혜교", "송")
        // 이 경우에도 p2.fname과 p2.lname의 값을 외부에서 가져올 수는 없습니다.
        // 정의된 greet 메소드를 출력합니다.
        println(s"② ${p2.greet}")          
        
        // ③ public한 read only(val) fullname을 가지는 클래스
        val p3 = new Person3("구", "진")
        println(s"③ ${p3.fullName}님께 인사합니다. ${p3.greet}")        
        
        // ④ val fname과 var lname을 가지는 클래스
        val p4 = new Person4("지원", "Kim") {  
            override def toString = s"$lname$fname"
        }  
        // val로 선언된 p4.fname과 var로 선언된 p4.lname을 외부에서 읽을 수 있음
        println(s"④ ${p4.lname}${p4.fname}") 
        
        // ⑤ Person4클래스를 이용해서 객체를 생성하지만, 해당 객체의 toString메소드만 오버라이드
        val p5 = new Person4("시진", "유") {  
            override def toString = s"$lname$fname"
        }  
        println(s"⑤ $p5") // 오버라이드된 toString형태로 출력
    }
}
```

#### getter와 setter

설명
```
자바와 달리 스칼라에서는 변수(val, var)와 메소드(def)는 같은 이름을 사용할 수 없습니다. 
예를 들어 자바에서는 int name;이라는 필드와 int name(){ return 0; }이라는 메소드가 
한 클래스에 있을 수 있지만, 스칼라에서는 안 됩니다.
그래서 JPerson.scala를 보면 필드 이름은 _name으로, setter는 name_으로, getter는 name으로 정의하고 있습니다.

자바 스타일의 getter와 setter가 필요하면 @BeanProperty를 활용하면 되는데요. 
SPerson.scala를 보면 getName과 setName이라는 메소드를 가지는 클래스를 한 줄로 간단히 만들고 있습니다.
```

코드
```
// 자바 스타일 클래스
class JPerson() {  
    var _name: String = null  
    def this(_name:String) = {  
        this()  
            this._name = _name  
    }  
    
    // 스칼라 스타일의 getter, setter   
    def name_=(_name:String) = this._name = _name  
    def name = this._name  
    
    // 자바 스타일의 getter, setter   
    def getName() = name  
    def setName(name:String) = this.name = name  
}
```
