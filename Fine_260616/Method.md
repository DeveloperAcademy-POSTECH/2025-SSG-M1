* 어떤 동작을 실행하는 코드의 묶음
* func 키워드로 만듦 => 특정 타입(struct, clas, enum과 같은 자료형)에 소속된 함수
* 
## 함수와의 구분
	* 함수(Function): 아무 데나 자유롭게 사용가능 (전역함수)
	* 메서드(Method): 특정 타입에 소속된 함수
	
             ┌──────────────┐
             │    함수       │
             └──────────────┘
                     ▲
          ┌──────────┴──────────┐
          │                     │
          전역 함수          메서드 (= 타입 안에 있음)
                             │
               ┌─────────────┬─────────────┐
               │             │             │
            struct         class          enum

예) 함수
func greet(name: String) {
    print("안녕, \(name)!")
}

예) 메서드
struct Person {
    var name: String

    // 이건 메서드예요!
    func greet() {
        print("안녕, 나는 \(name)이야!")
    }
}
* person이라는 타입(구조체) 안에 있음.
* person이라는 자료형에 소속된 함수 => 메서드

## 메서드가 필요한 이유
* 타입에 행동을 붙일 수 있기 때문에 => 어떤 데이터가 '할 수 있는 동작'을 함께 묶어두면 훨씬 직관적이고 깔끔하며 재사용이 쉬워지기 때문.
* 예) 강아지.run(), 사람.sayHello(), 계산기.add()
## **정리표**
| **구분** | **정의 위치**      | **부르는 방법** | **예시 코드**                    |
| ------ | -------------- | ---------- | ---------------------------- |
| 함수     | 아무데나 가능        | 이름()       | greet(name: "민수")            |
| 메서드    | 타입(struct 등) 안 | 타입.이름()    | person.greet() (person은 구조체) |

# 언제 사용하나?
* 버튼을 누를 때 - 클릭하면 어떤 동작을 하도록 만들기 위해
* 애니메이션 줄 때 - 값 바꾸고 애니메이션도 같이 실행하기 위해
* 값 계산할 때 - 똑같은 계산을 반복하지 않고 재사용하기 위해
* 뷰 업데이트 - 값이 바뀌면 화면도 바뀌게 연결할 수 있음.
# Method 기본 문법
1. 정의하기 (func로 선언)
	func Method이름(매개변수: 타입)-> 리턴타입 {
    // 실행할 코드
}
2. 호출하기 (필요한 때 사용)
	Method이름(매개변수)

|**요소**|**설명**|
|---|---|
|func|메서드를 만들 때 사용하는 키워드|
|이름|메서드를 호출할 때 사용하는 이름|
|매개변수|메서드가 작업할 때 필요한 값 (없어도 됨)|
|반환(return)|메서드가 계산하고 돌려주는 결과 값 (선택)|

예1) 기본 구조
func sayHello() {
    print("안녕!")
}

예2) 매개변수가 있는 Method
**struct** ContentView: View {
    // 메서드 정의: 이름을 받아 인사 출력
    **func** greet(name: String) {
        print("안녕, \(name)!")
    }

    // 화면 그리는 부분
    **var** body: **some** View {
        VStack(spacing: 20) {
            Button("Say Hello") {
                greet(name: "지민") // 콘솔에 "안녕, 지민!" 출력됨
            }
        }
        .padding()
    }
}

예3) 값을 돌려주는(return) Method
**struct** ContentView: View {
 **func** add(a: Int, b: Int) -> Int {
     **return** a + b
 }

    // 화면 그리는 부분
    **var** body: **some** View {
        VStack(spacing: 20) {
            Button("Add Numbers") {
             **let** result = add(a: 3, b: 5)
             print("결과는 \(result)입니다.")// 콘솔에 "결과는 8입니다." 출력됨
            }
        }
        .padding()
    }
}

예4) swiftUI 뷰 안에서 Method 사용
	버튼을 눌러서 점수를 올리는 메서드
struct ScoreView: View {
    @State private var score = 0

    func increaseScore() {
        score += 1
    }

    var body: some View {
        VStack {
            Text("점수: \(score)")
            Button("점수 올리기", action: increaseScore)
        }
    }
}

**Q.** 메서드는 꼭 뷰(struct) 안에 있어야 하나요?
아니요. struct, class, 또는 자유롭게 함수처럼 **전역에서도 만들 수 있어요.**
일반 계산, 날짜 포맷팅 등은 외부 함수로 빼도 됩니다.
다만 SwiftUI에서 **뷰와 연결된 동작이라면**, 뷰 안에 넣는 게 좋아요.

**Q.** 메서드 이름은 아무렇게나 지어도 돼요?
숫자로 시작하거나 공백이 들어가면 안 되고,
Swift 예약어는 피해야 해요. 보통 소문자로 시작하고 동사 형태로 짓는 게 좋아요.

**Q.** 메서드 안에서 다른 메서드 부를 수 있어요?
당연해요! 메서드끼리 서로 호출하며 큰 동작을 나눌 수 있어요.

# **✅ Swift에서 메서드와 비슷한 역할을 하는 것들**

| **종류**                            | **설명**                          |
| --------------------------------- | ------------------------------- |
| ✅ 함수 (Function)                   | 메서드와 거의 같은 개념. 구조체나 클래스 밖에서 정의됨 |
| ✅ 클로저 (Closure)                   | 이름 없는 함수처럼 사용되는 코드 덩어리          |
| ✅ 컴퓨티드 프로퍼티 (Computed Property)   | 값을 저장하지 않고 계산해서 돌려주는 속성         |
| ✅ 서브스크립트 (Subscript)              | 배열처럼 대괄호로 값을 꺼낼 수 있게 만드는 기능     |
| ✅ 연산자 오버로딩 (Operator Overloading) | +, *, == 등 연산자에 동작을 직접 정의함      |

## **1️⃣ 함수 (Function) – 메서드랑 거의 같음**
func add(a: Int, b: Int) -> Int {
    return a + b
}

let result = add(a: 3, b: 4)  // result = 7
- 함수는 **클래스나 구조체 안에 없어도** 정의 가능
- 메서드는 특정 타입에 묶여 있는 함수
## **2️⃣ 클로저 (Closure) – 이름 없는 작은 함수**
let sayHi = {
    print("안녕!")
}

sayHi()  // 클로저 실행됨
- 함수처럼 작동하지만 **이름이 없거나 변수에 저장 가능**
- func 없이 중괄호{} 만으로 만들어짐. - { print("안녕!") }
- 변수나 상수에 담아서 저장 가능. - sayHi라는 상수에 저장됨.
- 상수에 ()를 붙이면 클로저가 실행됨. - sayHi()
- SwiftUI의 .onTapGesture { ... }, .sheet { ... } 도 전부 클로저
- 왜 사용? - 짧게 쓸 수 있고, 다른 함수에 전달할 수 있어서 유연한 기능 작성에 좋음.
- 언제 사용? - SwiftUI, 애니메이션, 버튼 동작에 자주 사용.

## **클로저 vs 함수 차이 정리**
| **구분** | **함수 (Function)** | **클로저 (Closure)**      |
| ------ | ----------------- | ---------------------- |
| 정의 방식  | func 키워드 사용       | { } 중괄호만 사용            |
| 이름     | 필수                | 없어도 됨 (보통 변수에 저장함)     |
| 저장     | 함수는 직접 실행하거나 전달   | 클로저는 변수/상수에 저장해 재사용 가능 |

## **3️⃣ 컴퓨티드 프로퍼티 (Computed Property) – 읽을 때마다 계산하는 속성**
 **struct** Circle {
  **var** radius: Double
  **var** area: Double {
   **return** radius * radius * 3.14
  }
 }

 **var** body: **some** View {
  **let** c = Circle(radius: 10)
  
  VStack(spacing: 20) {
   Text("넓이: \(c.area)")  // "넓이: 314.0" () 없이 사용 - 메서드와 다른 점.
  }
  .padding()
 }
}
- area는 Computed property - 값을 저장해 두지 않고 필요할 때마다 계산해서 알려줌. 
- 메서드처럼 계산 결과를 주지만 **속성처럼 사용**됨 (값처럼 . 찍어서 씀)
|**이름**        |**저장함?**|**매번 계산함?**|**사용하는 법**         | 예
|저장 속성|✅         |❌                |circle.radius     | 종이에 '10'이라고 숫자를 써놓은 것
|계산 속성|❌         |✅                |circle.area        | 종이에 '10'이라고 쓰여있는 걸 보고 매번 계산기 두두려서 "314.0"을 보여주는 것
|메서드     |❌         |✅               |circle.getArea()| "계산기 켜서 직접 눌러주세요."

**Q.** 계산 속성은 항상 계산해요? 느려지진 않나요?
A. 네, 매번 계산해요. 가벼운 계산은 문제 없지만, 무거운 계산은 lazy var나 저장 속성으로 바꾸는 게 나을 수 있어요.

**Q.** 계산 속성에도 set을 쓸 수 있나요?
A. 네! get과 set을 함께 써서 읽고 쓸 수 있는 계산 속성도 만들 수 있어요.
var area: Double {
    get { ... }
    set { ... }
}

**Q.** 메서드로 해도 되는데 계산 속성을 쓰는 이유는?
A. 속성처럼 보이게 하면 **코드가 자연스럽고 읽기 쉬워져요.**
사람이 읽을 때 **값처럼 보이지만, 사실 계산돼서 똑똑한 코드가 되는 거죠.**

## **4️⃣ 서브스크립트 (Subscript) – 배열처럼 동작하게 만들기**
struct WordList {
    let words = ["apple", "banana", "cherry"]

    subscript(index: Int) -> String {
        return words[index]
    }
}

 **var** body: **some** View {
     **let** list = WordList()
     **let** secondWord = list[1] // "banana"

     VStack(spacing: 20) {
         Text("두 번째 단어는:")
         Text(secondWord)
             .font(.title)
             .foregroundColor(.purple)
     }
     .padding()
 }
}

- 메서드처럼 내부 로직을 갖고 있지만,
- **배열처럼 쓰이도록 만든 함수**
- 위의 예에서 words는 배열이지만, WordList는 배열이 아님. => WordList()[0] => 에러남. 
- subscript를 써서 WordList가 배열처럼 동작함.
## **5️⃣ 연산자 오버로딩 – 연산자를 함수처럼 정의하기**
 **struct** Point {
     **var** x: Int
     **var** y: Int
  
     // + 연산자 오버로딩: 두 Point를 더할 수 있게 만듦
     **static** **func** + (a: Point, b: Point) -> Point {
         **return** Point(x: a.x + b.x, y: a.y + b.y)
     }
 }

 **struct** ContentView: View {
     **var** body: **some** View {
         **let** p1 = Point(x: 1, y: 2)
         **let** p2 = Point(x: 3, y: 4)
         **let** p3 = p1 + p2  // Point(x: 4, y: 6)
         
         **return** VStack(spacing: 20) {
             Text("p1: (\(p1.x), \(p1.y))")
             Text("p2: (\(p2.x), \(p2.y))")
             Text("p1 + p2 = (\(p3.x), \(p3.y))")
         }
         .padding()
     }
 }
- + 기호는 사실 메서드처럼 작동함. 
- 원래 +는 숫자끼리만 더할 수 있지만, 이렇게 정의하면 Point끼리도 + 연산이 가능함. 좌표를 더해서 새로운 좌표를 만들도록 한 것. 
- 개발자가 직접 기능을 정의할 수 있음.
|**개념**               |**설명**
|Point 구조체  |좌표 (x, y)를 나타냄
|static func +|두 Point를 더할 수 있도록 + 연산자 동작 정의
|p1 + p2          |각각의 x, y 값을 더해서 새 Point 생성
|화면 출력         |결과를 Text로 표현해서 SwiftUI 화면에서 확인 가능

**Q** static이 왜 붙었어요?
A. 연산자 오버로딩은 타입 전체에 대한 동작이라서 static이 필요해요.
(인스턴스 하나가 아닌 Point 타입끼리 더하는 거니까요.)

**Q.** -, * 같은 다른 연산자도 오버로딩할 수 있어요?
A. 물론이죠! static func - (...) -> Point 도 만들 수 있어요.

**Q.** Swift가 왜 이렇게 연산자까지 만들 수 있게 해놨어요?
A. 숫자뿐만 아니라 구조체나 벡터, 좌표, 돈, 색상 등 **자연스럽게 더하고 빼고 비교**할 수 있게 하려고요.