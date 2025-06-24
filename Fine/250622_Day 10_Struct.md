# 1. [How to create your own structs](https://www.hackingwithswift.com/quick-start/beginners/how-to-create-your-own-structs)
* Struct(구조체): 고유한 변수와 함수를 갖춘 사용자 정의된, 복잡한 데이터 유형을 만들 수 있음.

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
* 함수를 호출하듯 새 앨범을 만듦 - 정의된 순서대로 각 상수에 대한 값을 제공하기만 하면 됨. 
* "Red"와"Wings"는 둘 다 같은 앨범 구조(Struct)에서 나오지만, 일단 생성하고 나면 두 개의 문자열을 생성하는 것처럼 분리됨.
* printSummary 함수를 실행해 보면 알 수 있음. - red는 "Red (2012)" by Taylor Swift를 출력하고, wings는 "Wings (2016)" by BTS를 출력함.

값을 변경해야 할 때는?
예) 필요에 따라 휴가를 사용할 수 있는 Employee Struct(구조체)
```swift
struct Employee {
    let name: String
    var vacationRemaining: Int

    func takeVacation(days: Int) {
        if vacationRemaining > days {
            vacationRemaining -= days
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
* Struct
```swift
mutating func takeVacation(days: Int) {
```
* 이제 코드가 빌드는 되지만, Swift는 상수인 구조체에서 takeVacation()을 호출하지는 못함.
```swift
var archer = Employee(name: "Sterling Archer", vacationRemaining: 14)
archer.takeVacation(days: 5)
print(archer.vacationRemaining)
```
* 이제 실행 가능. 그러나 var를 let으로 바꾸면 다시 실행 불가능.

-----
# 연관 개념들
* Property(속성): 구조체(Struct)에 속하는 변수(var)와 상수(let). (속성이나 특징)
* Method: 구조체에 속하는 함수
* Instance: 구조체에서 상수나 변수를 생성할 때
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

* 인스턴스와 프로퍼티 (예: 자동차)
	* 자동차 - 클래스 / 구조체  |  album
	* 인스턴스 - 내 차, 네 차    |  red, wings
	* 프로퍼티 - 색상, 모델, 제조사    | title, artist, year
		* 내 차 색상 - 빨간색, 네 차 색상 - 파란색 => 각 인스턴스마다 다른 프로퍼티 값을 가질 수 있음. => 인스턴스 프로퍼티
		* 바퀴 개수 - 모든 자동차공통됨 => 정적 프로퍼티(타입 프로퍼티) 

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

| 항목      | Tuple                  | Struct                |
| ------- | ---------------------- | --------------------- |
| 정의 방법   | 즉석에서 묶음                | 별도의 타입으로 정의           |
| 멤버 접근   | `.0`, `.1` 또는 이름 지정 가능 | 이름 지정 필수              |
| 메서드     | 없음                     | 있음                    |
| 초기화     | 기본 제공                  | 커스터마이즈 가능             |
| 용도      | 간단한 값 묶음, 반환 값 등 임시용   | 구조화된 모델 정의 및 기능 포함 가능 |
| 확장성/재사용 | 낮음                     | 높음                    |
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
```
func getUser() -> (String, Int) {
    return ("Soo", 29)
}

let result = getUser()
print("이름: \(result.0), 나이: \(result.1)")
```

* 구조체 예시
```
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

-----
# 2. [How to compute property values dynamically](https://www.hackingwithswift.com/quick-start/beginners/how-to-compute-property-values-dynamically)

##### 동적으로 계산되는 프로퍼티(Computed Property)
* 프로퍼티(property): 클래스나 구조체(struct), 열거형(enum) 안에 있는 값(속성).
* 이 프로퍼티는 크게 두 가지로 나뉨.
    •    저장 프로퍼티(stored property): 값을 직접 저장하는 속성. 변수 또는 상수.
    •    계산 프로퍼티(computed property): 값을 저장하지 않고, 필요할 때마다 계산해서 돌려주는 속성. 저장 프로퍼티와 함수의 조합(저장 프로퍼티처럼 접근하지만 함수처럼 작동함).

예) 직원의 남은 휴가 일수 계산
```swift
struct Employee {
    let name: String
    var vacationRemaining: Int
}

var archer = Employee(name: "Sterling Archer", vacationRemaining: 14)
archer.vacationRemaining -= 5
print(archer.vacationRemaining)
archer.vacationRemaining -= 3
print(archer.vacationRemaining)
```
위와 같이 하면 직원에게 14일의 휴가를 할당한 다음 휴가 일수가 주어들면서 휴가 일수를 빼나가는데, 원래 부여된 휴가 일수를 알 수 없게 됨.
```swift
struct Employee {
    let name: String
    var vacationAllocated = 14
    var vacationTaken = 0

    var vacationRemaining: Int {
        vacationAllocated - vacationTaken
    }
}
```
vacationRemaining: 실제 할당된 휴가에서 실제 사용한 휴가를 뺀 값을 계산.

```swift
var archer = Employee(name: "Sterling Archer", vacationAllocated: 14)
archer.vacationTaken += 4
print(archer.vacationRemaining)
archer.vacationTaken += 4
print(archer.vacationRemaining)
```

* vacationRemaining을 읽을 수는 있지만 쓸 수는 없음. vacationRemaining은 “계산 프로퍼티(computed property)“로, 값을 직접 저장하지 않고, 매번 계산해서 보여줌.
즉, 읽기(getter)는 가능하지만, 쓰기(setter)는 안 됨.

```
struct Employee {
    var name: String
    var vacationAllocated: Int
    var vacationTaken: Int = 0

    var vacationRemaining: Int {
        return vacationAllocated - vacationTaken
    }
}
```
이렇게 하면 vacationRemaining을 읽을 수는 있지만,
```
archer.vacationRemaining = 5 // 이렇게 직접 값을 넣으려고 하면 에러!
```
이렇게 쓸 수는 없음.
왜냐하면, “남은 휴가일수를 바꾼다”는 게 실제로 어떤 값을 바꿔야 하는지 Swift가 알 수 없기 때문.

##### getter와 setter란?
    •    getter: 값을 읽을 때 실행되는 코드 (예: vacationRemaining을 읽을 때)
    •    setter: 값을 쓸 때 실행되는 코드 (예: vacationRemaining에 값을 넣으려고 할 때)

getter만 있으면 읽기 전용.
setter까지 있으면 읽고 쓸 수 있음.

##### vacationRemaining의 setter를 만들 때 고민할 점
만약 vacationRemaining에 값을 넣을 수 있게 하려면, setter를 만들어야 함.
그런데, vacationRemaining을 바꾼다는 건 실제로 어떤 값을 바꿔야 하나?
    •    vacationAllocated(할당된 휴가일수)를 바꿔야 할까?
    •    vacationTaken(사용한 휴가일수)를 바꿔야 할까?
예를 들어, vacationRemaining을 5로 바꾼다고 하면,
    •    할당된 휴가일수는 그대로 두고, 사용한 휴가일수를 바꿔서 남은 휴가가 5가 되게 할 수도 있고,
    •    혹은 사용한 휴가일수는 그대로 두고, 할당된 휴가일수를 바꿀 수도 있음.
이렇게 여러 가지 방법이 있기 때문에, setter를 직접 구현해줘야 Swift가 어떻게 해야 하는지 알 수 있음.
예) vacationTaken을 바꾸는 setter
아래처럼 setter를 만들어주면, vacationRemaining에 값을 넣을 수 있음.
```
struct Employee {
    var name: String
    var vacationAllocated: Int
    var vacationTaken: Int = 0

    var vacationRemaining: Int {
        get {
            return vacationAllocated - vacationTaken
        }
        set {
            vacationAllocated = vacationTaken + newValue
        }
    }
}
```

```swift
var archer = Employee(name: "Sterling Archer", vacationAllocated: 14)
archer.vacationTaken += 4
archer.vacationRemaining = 5
print(archer.vacationAllocated)
```

라고 하면, vacationAllocated 값이 자동으로 바뀌어서, 남은 휴가가 5일이 되도록 맞춰짐.

##### 정리
    •    vacationRemaining은 계산 프로퍼티이기 때문에, 기본적으로 읽기만 가능(getter만 있을 때).
    •    vacationRemaining에 값을 넣으려면, setter(쓰기용 코드)를 구현해야 함.
    •    setter를 만들 때는, 어떤 값을 바꿀지(휴가 할당량? 사용량?)를 직접 정해줘야 함.
    •    setter와 getter를 모두 구현하면, 읽고 쓰는 것이 모두 가능함.

-----

1. 프로퍼티란?
Swift에서 프로퍼티(property)는 구조체(struct)에 정보를 붙여주는 역할을 함.
예) 사람 정보를 담는 구조체가 있다면 이름(name), 나이(age) 같은 값이 프로퍼티.

2. 프로퍼티의 두 가지 종류
Swift에는 프로퍼티가 크게 두 가지가 있음.
(1) 저장 프로퍼티(stored property)
    •    값을 나중에 사용하기 위해 메모리에 저장해 둠.
    •    값을 바꿀 수도 있고, 읽을 수도 있음.
    •    예시:
```
struct User {
   var name: String // 저장 프로퍼티
   var age: Int     // 저장 프로퍼티
}
```
(2) 계산 프로퍼티(computed property)
    •    값을 직접 저장하지 않고, 호출될 때마다 다시 값을 계산함.
    •    실제로는 함수처럼 동작하지만, 프로퍼티처럼 사용.
    •    예시:
```
struct Rectangle {
   var width: Double
   var height: Double
   var area: Double {
         return width * height // 계산 프로퍼티
   }
}
```

3. 계산 프로퍼티는 사실상 함수다?
계산 프로퍼티는 값을 저장하지 않고, 매번 계산해서 돌려줌.
실제로는 함수처럼 동작하지만, 프로퍼티처럼 점(.)으로 접근해서 쓸 수 있음.

4. 언제 어떤 프로퍼티를 써야 할까?
(1) 값이 자주 바뀌지 않고, 자주 읽는 경우 → 저장 프로퍼티
    •    값을 메모리에 저장해 두니까, 읽을 때마다 계산하지 않아 빠름.
    •    예: 이름, 나이, 이메일 주소 등
(2) 값이 다른 프로퍼티에 따라 계속 달라지는 경우 → 계산 프로퍼티
    •    항상 최신 상태를 반영해야 할 때 유용.
    •    예: 넓이(area)는 width와 height가 바뀌면 자동으로 바뀌어야 하니까 계산 프로퍼티가 좋음.
(3) 성능(퍼포먼스)도 고려해야 함
    •    저장 프로퍼티는 값을 한 번만 계산해서 저장하니, 자주 읽을 때 빠름.
    •    계산 프로퍼티는 읽을 때마다 계산하니, 자주 읽으면 느려질 수 있음.
    •    반대로, 거의 안 읽는 값이라면 굳이 저장하지 않고 계산 프로퍼티로 두는 게 메모리를 아낄 수 있음.
    
5. 의존성(dependency)도 중요한 기준
    •    어떤 프로퍼티가 다른 프로퍼티 값에 따라 달라진다면, 계산 프로퍼티로 만들어야 항상 최신 값을 얻을 수 있음.
    •    저장 프로퍼티로 만들면, 값이 바뀔 때마다 일일이 값을 새로 계산해서 저장해줘야 하니 번거롭고, 실수할 수 있음.
    
6. 추가 팁: lazy 프로퍼티와 프로퍼티 옵저버
    •    lazy 프로퍼티: 잘 안 쓰는 값을 저장 프로퍼티로 만들 때, 처음 사용할 때 한 번만 계산해서 저장해두는 방법. (메모리와 성능을 모두 챙길 수 있음)
    •    프로퍼티 옵저버: 저장 프로퍼티의 값이 바뀔 때마다 특정 코드를 실행할 수 있게 해줌. (의존성 문제를 어느 정도 해결)
    
7. 정리
    •    저장 프로퍼티: 값을 저장해두고, 자주 읽을 때 빠름.
    •    계산 프로퍼티: 값을 저장하지 않고, 읽을 때마다 계산해서 항상 최신 상태를 반영.
    •    선택 기준: 값이 자주 바뀌지 않고 자주 읽으면 저장 프로퍼티, 다른 값에 따라 달라지면 계산 프로퍼티.
    •    성능과 의존성도 고려해야 함.
##### 계산 프로퍼티의 장점
    •    값이 바뀔 때마다 자동으로 최신 값을 계산할 수 있음.
    •    여러 저장 프로퍼티를 조합해서 새로운 값을 만들 수 있음.
    •    속성이 실제로 저장되지 않으니, 메모리도 절약할 수 있음.
##### 중요 포인트 요약
    •    계산 프로퍼티는 값을 저장하지 않고, 필요할 때마다 코드를 실행해 값을 계산.
    •    읽기 전용(getter만) 또는 읽고 쓰기(getter + setter) 모두 가능함.
    •    계산 프로퍼티를 사용하면, 코드가 더 깔끔하고, 실시간으로 최신 값을 얻을 수 있음.

-----
# [How to take action when a property changes](https://www.hackingwithswift.com/quick-start/beginners/how-to-take-action-when-a-property-changes)

* 속성 관찰자(Property observer): 속성이 변경될 때 실행되는 특수 코드. 
    * 이 관찰자는 두 가지 형태를 가짐. 
        * `didSet`: 속성이 방금 변경되었을 때 실행되는 관찰자 
        * `willSet`: 속성이 변경되기 _전에_ 실행되는 관찰자

```swift
struct Game {
    var score = 0
}

var game = Game()
game.score += 10
print("Score is now \(game.score)")
game.score -= 3
print("Score is now \(game.score)")
game.score += 1
```

Game 구조체에서 점수 수정. 점수가 변경될 때마다 `print()`변경 사항을 추적할 수 있도록 줄을 추가함. 그런데 마지막에 점수가 변경되었는데, 점수가 출력되지 _않음, 실수.

속성 관찰자를 사용하면 속성이 변경될 때마다(어디에서 변경되든) 항상 일부 코드를 실행하게 함.
```swift
struct Game {
    var score = 0 {
        didSet {
            print("Score is now \(score)")
        }
    }
}

var game = Game()
game.score += 10
game.score -= 3
game.score += 1
```