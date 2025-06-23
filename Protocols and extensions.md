**프로토콜은 코드에 대한 계약과 같다. 필요한 기능과 방법을 지정하고, 이를 준수하는 유형은 이를 구현해야 한다.

Vehicle 프로토콜을 다음과 같이 정의할 수 있다.
```swift
protocol Vehicle {
    func estimateTime(for distance: Int) -> Int
    func travel(distance: Int)
}
```

- protocol 과 프로토콜명을 쓰면 새 프로토콜을 생성할 수 있다. 새로운 유형이므로, 대문자로 시작하는 camel case를 사용해야 한다.
- 프로토콜 내부에는 우리가 사용할 메서드를 나열한다.
- 이 메서드들은 어떤 코드도 안에 지니고 있지 않다. function body는 여기 쓰지 않는다. 대신 메서드명, 매개변수, 그리고 변환 타입을 작성한다. 

프로토콜은 존재해야 하는 전체 기능 범위를 지정하지 않고 최소한의 기능만 지정한다. 이는 프로토콜을 준수하는 새로운 유형을 생성할 때 필요에 따라 모든 종류의 다른 속성과 메서드를 추가할 수 있음을 의미한다.

예를 들어 Vehicle을 준수하는 Car Struct를 만들 수 있다.

```swift
struct Car: Vehicle {
    func estimateTime(for distance: Int) -> Int {
        distance / 50
    }

    func travel(distance: Int) {
        print("I'm driving \(distance)km.")
    }

    func openSunroof() {
        print("It's a nice day!")
    }
}
```

- Car 뒤에 : 을 붙여 Vehicle을 준수한다고 표시할 수 있다. Subclass를 표시하듯이 말이다.
- Vehicle에 나열했던 메서드는 반드시 모두 Car에 있어야 한다. 조금이라도 다른 이름을 지니고 있거나, 다른 매개변수를 받거나, 다른 반환 타입을 갖는 등의 차이가 있다면, 프로토콜을 준수한다고 여기지 않을 것이다.
- Car 에 들어있는 메서드는 프로토콜에 정의한 메서드의 실제 실행에 대해 설명할 것이다. 
- opensunroof() 메서드는 Vehicle 프로토콜에서 온 게 아니며 많은 교통수단이 선루프가 없기 때문에 말이 되지 않는다. 하지만 프로토콜은 최소한의 반드시 준수해야 하는 타입만 정의하기 때문에, 필요한 것을 추가로 정의해도 괜찮다.

 Car에 추가한 메서드들을 사용하도록 commute() 함수를 써보자.

```swift
func commute(distance: Int, using vehicle: Car) {
    if vehicle.estimateTime(for: distance) > 100 {
        print("That's too slow! I'll try a different vehicle.")
    } else {
        vehicle.travel(distance: distance)
    }
}

let car = Car()
commute(distance: 100, using: car)
```

해당 코드는 모두 작동하지만 여기서 프로토콜은 실제로 어떤 값도 추가하지 않는다. Car 내부에 매우 특정한 두 가지 메서드를 구현하게 되었지만 프로토콜을 추가하지 않고도 그렇게 할 수 있는데 굳이 귀찮게 할 필요가 있을까?

Vehicle을 준수하는 모든 유형이 estimateTime() 및 travel() 메서드를 모두 구현해야 한다는 사실을 알기 때문에, Vehicle을 매개변수 유형으로 사용할 수 있다. 함수를 다음과 같이 다시 작성할 수 있다.

```swift
func commute(distance: Int, using vehicle: Vehicle) {
```

이제 우리는 해당 유형이 Vehicle 프로토콜을 준수하는 한 모든 유형의 데이터로 이 함수를 호출할 수 있다고 말한다. 함수의 본문은 변경할 필요가 없다. 

이것이 왜 유용한지 여전히 궁금하다면 다음 struct를 살펴보자.

```swift
struct Bicycle: Vehicle {
    func estimateTime(for distance: Int) -> Int {
        distance / 10
    }

    func travel(distance: Int) {
        print("I'm cycling \(distance)km.")
    }
}

let bike = Bicycle()
commute(distance: 50, using: bike)
```

이제 Vehicle을 준수하는 두 번째 struct가 생겼고, 여기서 프로토콜의 힘이 명백해진다. 이제 Car나 Bicycle을 commte() 함수에 전달할 수 있다. 내부적으로 함수는 원하는 모든 로직을 가질 수 있으며, estimateTime 또는 travel을 호출하면 적절한 로직을 사용한다. car를 통하면 "I'm driving"라고 말하고, bicycle을 통과하면 "I'm cycling" 이라고 말한다.

따라서 프로토콜을 사용하면 정확한 유형보다는 작업하려는 기능의 종류에 대해 이야기할 수 있다. 이 매개변수는 자동차여야 한다, 라고 말하는 대신, 이 매개변수는 이동시간을 추정하고 새로운 위치로 이동할 수 있는 한 무엇이든 될 수 있다, 라고 말할 수 있다.

메서드 뿐만 아니라 존재해야 하는 속성을 설명하는 프로토콜을 작성할 수도 있다. 이렇게 하려면 var를 쓰고 속성 이름을 쓴 다음, 읽기 및 쓰기 가능 여부를 나열하면 된다.

예를 들어 Vehicle을 준수하는 모든 유형은 다음과 같이 이름과 현재 승객수를 지정해야 한다고 정의할 수 있다.

```swift
protocol Vehicle {
    var name: String { get }
    var currentPassengers: Int { get set }
    func estimateTime(for distance: Int) -> Int
    func travel(distance: Int)
}
```

- name이라는 읽을 수 있는 문자 데이터를 추가한다. 상수일 수도 있으며, getter가 있는 계산된 속성(**다른 속성을 기반**으로 해당 속성 값이 결정된다)일 수도 있다.
- currentPassengers라는 읽고 쓸 수 있는 정수 데이터를 추가한다. 변수일 수 있으며, getter와 setter가 있는 계산된 속성일 수 있다.

\* getter: 외부에서 객체의 데이터를 읽을 때 사용하는 메서드 
	(get + 필드이름(대문자시작)), return 필요
\*setter: 외부에서 객체의 데이터를 수정할 때 사용하는 메서드
	(set + 필드이름(대문자시작)), 매개변수 필요

프로토콜이 메서드에 대한 구현을 제공할 수 없는 것처럼 프로토콜에 기본값을 제공할 수 없다. 따라서 두 데이터 모두에 유형 선언이 필요하다.

**불투명한 반환 유형을 사용하면 코드에서 일부 정보를 숨길 수 있다. 이는 향후 변경에 대한 유연성을 유지하고 싶다는 의미일 수도 있지만, 거대한 반환 유형을 작성할 필요가 없다는 의미이기도 하다.

Tip: 불투명 반환 타입이 어떻게 작동하는지 자세히 이해할 필요는 없으며, 이것이 존재하고 매우 구체적인 작업을 수행한다는 것만 알면 된다. 

```swift
func getRandomNumber() -> Int {
    Int.random(in: 1...6)
}

func getRandomBool() -> Bool {
    Bool.random()
}
```
Int와 Bool은 모두 Equatable이라는 공통 프로토콜을 준수한다. 이는 동일성을 비교할 수 있음을 의미한다. 

Equatable 프로토콜을 사용하면 다음과 같이 \==을 사용할 수 있게 해준다.

```swift
print(getRandomNumber() == getRandomNumber())
```

둘 모두 Equatable을 준수하기 때문에, 다음과 같이 Equatable 값을 반환하도록 함수를 수정해 볼 수 있을 것 같다.

```swift
func getRandomNumber() -> Equatable {
    Int.random(in: 1...6)
}

func getRandomBool() -> Equatable {
    Bool.random()
}
```

그러나 둘 다 Equatable을 따르지만 이렇게 바꿔 사용할 수 없다. 컴파일 오류가 난다.

함수에서 프로토콜을 반환하면 정보를 숨길 수 있기 때문에 유용하다. 반환되는 정확한 유형을 명시하기 보다는 반환되는 기능에 집중할 수 있다. 

이러한 방식으로 정보를 숨기는 것은 유용하지만 Equatable에서는 서로 다른 항목을 비교할 수 없다. 두 개의 정수를 얻기 위해 getRandomNumber()를 두 번 호출하더라도 정확한 데이터 유형을 숨겼기 때문에 비교할 수 없다. 

두 함수를 불투명한 반환 유형으로 업그레이드하려면 다음과 같이 반환 유형 앞에 some 키워드를 추가하자.

```swift
func getRandomNumber() -> some Equatable {
    Int.random(in: 1...6)
}

func getRandomBool() -> some Equatable {
    Bool.random()
}
```

이제 getRandomNumber()를 두 번 호출하고 \==를 사용하여 결과를 비교할 수 있다. 우리의 관점에서 보면 여전히 Equatable 데이터가 일부만 있지만 Swift는 그 뒤에 실제로 두 개의 정수가 있다는 사실을 알고 있다.

Vehicle을 반환한다는 것은 "Vehicle 중 하나이지만, 무엇인지는 모른다"를 의미하는 한편, Some Vehicle을 반환한다는 것은 "특정 종류의 Vehicle 이지만, 무엇인지 말하고 싶지 않다"를 의미한다.

**확장 기능을 사용하면 자체 사용자 정의 유형이나 Swift의 내장 유형에 기능을 추가할 수 있다. 이는 메서드를 추가하는 것을 의미할 수도 있지만 계산된 속성을 추가할 수도 있다.

이를 설명하기 위해 TrimmingCharacters(in:)이라는 유용한 문자열 메서드를 소개하고 싶다. 이렇게 하면 문자열의 시작이나 끝에서 영숫자 문자, 십진수 또는 가장 일반적으로 공백 및 새 줄과 같은 특정 종류의 문자가 제거된다.

Whitespce(공백)은 공백 문자, 탭 문자 및 이 두 문자의 다양한 변형을 가리키는 일반적인 용어이다. 새 줄은 텍스트의 줄 바꿈으로 간단하게 들릴 수 있지만 실제로는 이를 만드는 단 하나의 방법이 없다. 따라서 새 줄을 자르라고 요청하면 자동으로 모든 변형이 처리된다.

```swift
var quote = "   The truth is rarely pure and never simple   "
let trimmed = quote.trimmingCharacters(in: .whitespacesAndNewlines)
```

이를 아래와 같은 확장으로 표현할 수 있다.

```swift
extension String {
    func trimmed() -> String {
        self.trimmingCharacters(in: .whitespacesAndNewlines)
    }
}
```

- Swift에 기존 유형에 기능을 추가하고 싶다고 알려주는 Extension 키워드부터 시작한다.
- 어떤 유형인지 쓴다. String에 기능을 추가하는 것이다.
- 이제 중괄호를 열고 마지막 닫는 중괄호까지의 모든 코드를 문자열에 추가한다.
- 새로운 문자열을 반환하는 Trimmed()라는 새로운 메서드를 추가하고 있다.
- 그 안에서 TrimmingCharacters(in:)를 호출하여 그 결과를 다시 보낸다.
- 여기서 self를 어떻게 사용할 수 있는지 주목하세요. 자동으로 현재 문자열을 참조한다. 이는 현재 문자열 확장에 있기 때문에 가능하다.

extension에는 전역 함수 기능에 비해 다음과 같은 여러 가지 이점이 있다.

- quote을 입력할 때. Xcode는 확장에 추가한 모든 메소드를 포함하여 문자열에 대한 메소드 목록을 표시한다. 이렇게 하면 추가 기능을 쉽게 찾을 수 있다.
- 전역 함수를 작성하면 코드가 다소 지저분해진다. 정리하기 어렵고 추적하기 어렵습니다. 반면 확장은 확장하는 데이터 유형에 따라 자연스럽게 그룹화된다.
- 확장 메소드는 원래 유형의 전체 부분이므로 해당 유형의 내부 데이터에 대한 전체 액세스 권한을 갖는다. 이는 예를 들어 개인 액세스 제어로 표시된 속성과 메서드를 사용할 수 있음을 의미한다.

게다가 확장 기능을 사용하면 값을 제자리에서 수정하는 것이 더 쉬워진다. 즉, 새 값을 반환하는 대신 값을 직접 변경하는 것이 가능하다.

예를 들어 이전에는 공백과 개행 문자가 제거된 새 문자열을 반환하는 Trimmed() 메서드를 작성했지만 문자열을 직접 수정하려면 다음을 확장에 추가할 수 있다.

```swift
mutating func trim() {
    self = self.trimmed()
}
```

quote 문자열은 변수로 생성되었기 때문에 다음과 같이 해당 위치에서 잘라낼 수 있다.

```swift
quote.trim()
```

이제 메서드 이름이 어떻게 약간 다른지 확인하라. 새 값을 반환할 때는 Trimmed()를 사용했지만 문자열을 직접 수정할 때는 Trim()을 사용했다. 이는 의도적이며 Swift 디자인 지침의 일부이다. 값을 제자리에서 변경하지 않고 새 값을 반환하는 경우 reversed()와 같은 ed 또는 ing와 같은 단어 끝을 사용해야 한다.

Tip: 이전에 배열의 sorted() 메서드를 소개했다. 이제 이 규칙을 알았으므로 변수 배열을 생성하는 경우 새로운 복사본을 반환하는 대신 해당 배열에 sort()를 사용하여 배열을 정렬할 수 있다는 것을 알아야 한다.

**프로토콜 확장을 사용하면 여러 유형에 기능을 한 번에 추가할 수 있다. 프로토콜에 속성과 메서드를 추가할 수 있으며, 이를 준수하는 모든 유형이 이에 액세스할 수 있다.

```swift
let guests = ["Mario", "Luigi", "Peach"]

if guests.isEmpty == false {
    print("Guest count: \(guests.count)")
}
```

나는 이러한 접근 방식 중 하나를 별로 좋아하지 않는다. 왜냐하면 "배열이 비어 있지 않으면"은 자연스럽게 읽히지 않기 때문이다.

다음과 같이 매우 간단한 Array 확장을 사용하여 이 문제를 해결할 수 있다.

```swift
extension Array {
    var isNotEmpty: Bool {
        isEmpty == false
    }
}
```

이제 더 이해하기 쉬운 코드를 쓸 수 있다:

```swift
if guests.isNotEmpty {
    print("Guest count: \(guests.count)")
}
```

하지만 더 잘 할 수 있다. 방금 isNotEmpty를 배열에 추가했다. 그런데 set와 Dictionary은 어떨까? 물론 반복해서 코드를 확장에 복사할 수도 있지만 더 나은 솔루션이 있다. Array, Set 및 Dictionary는 모두 Collection이라는 내장 프로토콜을 준수하며 이를 통해 contain(), sorted(), reversed() 등과 같은 기능을 사용할 수 있다.

Collection에는 필수적으로 isEmpty 속성이 있어야 한다. 따라서 Collection에 확장을 작성하면 isEmpty에 계속 액세스할 수 있다. 이는 코드에서 Array를 Collection으로 변경하여 다음을 얻을 수 있음을 의미한다.

```swift
extension Collection {
    var isNotEmpty: Bool {
        isEmpty == false
    }
}
```

한 단어만 변경하면 이제 배열, 세트, ​​사전은 물론 Collection을 준수하는 다른 유형에서도 isNotEmpty를 사용할 수 있다. 