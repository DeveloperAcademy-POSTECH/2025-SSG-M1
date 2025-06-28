# 1. [How to create your own structs](https://www.hackingwithswift.com/quick-start/beginners/how-to-create-your-own-structs)

* **Struct(구조체)**: 고유한 변수와 함수를 갖춘 사용자 정의된, 복잡한 데이터 유형을 만들 수 있음.

```swift
struct Album {
    let title: String
    let artist: String
    let year: Int

    func printSummary() {
        print("\(title) (\(year)) by \(artist)")
    }
}
```

* 여기에서 Album은 String이나 Int와 같이 만들고, 값을 할당하고, 복사하는 등의 작업을 할 수 있음. 
  예) 앨범을 여러 개 만든 다음, 각 앨범의 값을 출력하고 함수를 호출할 수 있음.

```swift
let red = Album(title: "Red", artist: "Taylor Swift", year: 2012)
let wings = Album(title: "Wings", artist: "BTS", year: 2016)

print(red.title)
print(wings.artist)

red.printSummary()  // "Red (2012)" by Taylor Swift 
wings.printSummary()  // "Wings (2016)" by BTS
```

* 함수를 호출하듯 새 앨범을 만듦. - 정의된 순서대로 각 상수에 대한 값을 제공하기만 하면 됨. 
* "Red"와"Wings"는 둘 다 같은 앨범 구조(Struct)에서 나오지만, 일단 생성하고 나면 두 개의 문자열을 생성하는 것처럼 분리됨.
* printSummary 함수를 실행해 보면 알 수 있음.
  - red는 "Red (2012)" by Taylor Swift를 출력하고, wings는 "Wings (2016)" by BTS를 출력함.

* 값을 변경해야 할 때는? => "Mutating func" 사용 
예) 필요에 따라 휴가를 사용할 수 있는 Employee Struct(구조체)
```swift
struct Employee {
    let name: String
    var vacationRemaining: Int

    func takeVacation(days: Int) {
        if vacationRemaining > days {
            vacationRemaining -= days  // 이 부분이 값을 변경하려고 하기 때문에 오류 발생
            print("I'm going on vacation!")
            print("Days remaining: \(vacationRemaining)")
        } else {
            print("Oops! There aren't enough days remaining.")
        }
    }
}
```
* 위의 코드는 동작하지 않음.
* let을 사용하여 직원을 상수로 생성하면 Swift는 직원과 모든 데이터를 상수로 만듦. 함수를 호출하는 것은 괜찮지만, 해당 함수는 구조체의 데이터를 변경할 수 없어야 함. 왜냐하면 상수로 만들었기 때문.
  => 구조체에 속한 데이터를 변경하는 함수는 다음과 같이 특수한 변형(mutating) 키워드로 표시해야 함.

```swift
Struct Employee {

}

mutating func takeVacation(days: Int) {
```
* 이제 코드가 빌드는 되지만, Swift는 상수인 구조체에서 takeVacation()을 호출하지는 못함.

```swift
var archer = Employee(name: "Sterling Archer", vacationRemaining: 14)
archer.takeVacation(days: 5) // 이 부분 때문에 let 사용하면 안 됨
print(archer.vacationRemaining)
```
* 이제 실행 가능. 그러나 var를 let으로 바꾸면 다시 실행 불가능.

-----
# 연관 개념들

* Property(속성): 구조체(Struct)에 속하는 변수(var)와 상수(let). (속성이나 특징)
* Method: 구조체에 속하는 함수
* Instance: 구조체에서 상수나 변수를 생성할 때
* 인스턴스와 프로퍼티 (예: 자동차)
	* 자동차 - 클래스 / 구조체  |  album
	* 인스턴스 - 내 차, 네 차    |  red, wings
	* 프로퍼티 - 색상, 모델, 제조사    | title, artist, year
		* 내 차 색상 - 빨간색, 네 차 색상 - 파란색 => 각 인스턴스마다 다른 프로퍼티 값을 가질 수 있음. => 인스턴스 프로퍼티
		* 바퀴 개수 - 모든 자동차공통됨 => 정적 프로퍼티(타입 프로퍼티) 
	
* 구조체의 인스턴스를 생성할 때는 다음과 같은 초기화 함수를 사용함.
  예) Album(title: "Wings", artist: "BTS", year: 2016) - 구조체를 함수처럼 취급하고 매개변수를 전달. 이는 일종의 문법적 편의(syntactic sugar)라고 할 수 있음. Swift는 구조체 내부에 init()이라는 특수 함수를 자동으로 생성하여 구조체의 모든 속성을 매개변수로 사용. 아래 두 코드를 자동으로 동일한 코드로 처리함.

```swift
var archer1 = Employee(name: "Sterling Archer", vacationRemaining: 14)
var archer2 = Employee.init(name: "Sterling Archer", vacationRemaining: 14)
```

```swift
let name: String
var vacationRemaining = 14

let kane = Employee(name: "Lana Kane")
let poovey = Employee(name: "Pam Poovey", vacationRemaining: 35)
```
* 상수 속성에 기본값을 할당하면 해당 값이 초기화 프로그램에서 완전히 제거됨(값 변경 불가능). 기본값을 할당하면서도 필요할 때 재정의할 수 있는 가능성을 남겨두려면 var 속성을 사용할 것.

-----
# [What’s the difference between a function and a method?](https://www.hackingwithswift.com/quick-start/understanding-swift/whats-the-difference-between-a-function-and-a-method)

* 공통점: 함수, 메서드 모두 기능의 일부에 이름을 지정하고 반복적으로 실행.
* 차이점
    * 메서드: 구조체, 열거형, 클래스와 같은 타입에 속함.
    * 함수: 타입에 속하지 않음.
* 메서드의 장점
    * 해당 유형 내의 다른 속성과 메서드를 참조할 수 있음. 
    * _네임스페이스 오염을_ 방지
        * 함수를 그냥 만들면 이름이 코드 전체에서 예약되어 네임스페이스 오염이 생김. 100개의 함수를 만들면 100개의 이름이 생김. 예) wakeUp() => 코드 전체에서 wakeUp이라는 함수 이름이 예약됨.
        * 메서드로 만들면, 객체 안에서만 의미가 있으니, 코드 전체에 이름이 퍼지지 않고 오염이 줄어듦. 예) someUser.wakeUp() - wakeUp이 코드 전체가 아니라 someUser 안에서만 의미를 가짐. someUser.wakeUp(), otherUser.wakeUp() 과 같은 식으로 구분 가능.
        * 그래서 많은 기능을 메서드로 만들면, 이름 충돌이나 헷갈림을 줄일 수 있음.

-----
# [What’s the difference between a struct and a tuple?](https://www.hackingwithswift.com/quick-start/understanding-swift/whats-the-difference-between-a-struct-and-a-tuple)

* 공통점: 튜플, 구조체 모두 하나의 변수에 여러 개의 서로 다른 이름을 가진 값을 저장할 수 있게 해 줌.
* 차이점
    * 튜플: "그냥 묶자" - **간단한** 값 모음용. 함수 반환, **임시** 데이터 처리
    * 구조체: "설계하자" - 기능과 함께 데이터를 구조화해서 관리.

| 항목      | Tuple                   | Struct                 |
| ------- | ----------------------- | ---------------------- |
| 정의 방법   | 즉석에서 묶음                 | 별도의 타입으로 정의            |
| 멤버 접근   | `.0`, `.1` 또는 이름 지정 가능  | 이름 지정 필수               |
| 메서드     | 없음                      | 있음                     |
| 초기화     | 기본 제공                   | 커스터마이즈 가능              |
| 용도      | 간단한 값 묶음, 반환 값 등 임시용    | 구조화된 모델 정의 및 기능 포함 가능  |
| 확장성/재사용 | 낮음                      | 높음                     |
* 튜플(Tuple): 여러 값을 간단하게 묶어 임시로 사용하고 싶을 때 사용.
        * 특징: 
            * 간단한 값 묶음. 
            * 임시/간단한 작업에 적합. 
            * 메서드, 초기화 함수 없음.
            * 타입을 새로 정의하지 않고 즉석에서 사용하는 용도
        * 적절한 상황
            * 함수에서 여러 값을 한 번에 반환할 때
            * 임시로 두 개의 값을 묶고 싶은 경우

* 구조체(Struct): 데이터를 구조적으로 설계하고, 관련된 기능(메서드)까지 함께 담고 싶을 떄 사용
    * 특징:
        * 타입을 정의하는 것, 새로운 데이터 모델을 만드는 방식
        * 프로퍼티 외에 메서드, 이니셜라이저, 프로토콜 채택 등 기능 확장 간.ㅇ
        * Codable, Equatable, Identifiable 등 다양한 프로토콜과 함께 사용 가능.
        * 앱 내에서 재사용, 유지보수, 확장성에 유리.
    * 적절한 상황
        * 사용자, 상품, 책 같은 실제 모델을 정의할 때
        * 데이터에 기능이나 행동(method)을 같이 정의하고 싶을 때
        * 앱 구조를 설계할 떄 기본 단위로 활용.

* 튜플 예시
```swift
func getUser() -> (String, Int) {
    return ("Soo", 29)
}

let result = getUser()
print("이름: \(result.0), 나이: \(result.1)")
```

* 구조체 예시
```swift
struct User {
    let name: String
    let age: Int
}

func getUser() -> User {
    return User(name: "Soo", age: 29)
}

let result = getUser()
print("이름: \(result.name), 나이: \(result.age)")
```

* Struct
```swift
struct User {
    var name: String
    var age: Int
    var city: String
}

func authenticate(_ user: User) { ... }
func showProfile(for user: User) { ... }
func signOut(_ user: User) { ... }
```

* Tuple 
```swift
func authenticate(_ user: (name: String, age: Int, city: String)) { ... }
func showProfile(for user: (name: String, age: Int, city: String)) { ... }
func signOut(_ user: (name: String, age: Int, city: String)) { ... }
```