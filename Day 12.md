**==1. 어떻게 당신만의 class를 만들까?==**
스위프트는 String, Int, Double, Array 등의 데이터 타입을 저장하기 위해 Structs를 사용한다. 하지만 이를 저장하는 다른 방법이 있는데, 바로 Class이다. class와 sturct는 공통점이 많지만 매우 다른 부분도 있다.

먼저, 공통점은 다음과 같다.
 - 이름을 지정하고 생성할 수 있다.
 - property observer와 access를 포함해, property와 method를 추가할 수 있다. 
 - custom initializer를 생성해 무엇이든 원하는 새로운 instances를 찾을 수 있다.

중요한 다섯 가지 차이점은 아래와 같다.
 - 한 클래스를 다른 클래스의 기능을 기반으로 구축하여 해당 클래스의 모든 속성과 메서드를 시작점으로 얻을 수 있다. 일부 메서드를 선택적으로 재정의하려는 경우에도 가능하다.
 - 첫 번째 포인트 때문에 Swift는 클래스에 대한 멤버별 초기화를 자동 생성하지 않는다. 따라서 직접 초기화 프로그램을 작성하거나 모든 속성에 기본값을 할당해야 한다.
 - 클래스의 인스턴스를 복사하면, 두 복사본 모두 동일한 데이터를 공유한다. 한 복사본을 변경하면 다른 복사본도 변경된다.
 - 클래스 인스턴스의 최종 복사본이 파괴되면 Swift는 선택적으로 Deinitializer라는 특수 함수를 실행할 수 있다.
 - 클래스를 상수(constant)로 만들더라도 클래스의 속성이 변수라면 이를 변경할 수 있다.

structs가 있는데 왜 classes가 필요한지 의문이 들 수 있다. 그러나 SwiftUI 는 class를 3가지 이유로 자주 사용한다: class의 복사본은 모두 같은 데이터를 공유한다. 즉, 당신의 앱에서 많은 부분이 같은 정보를 공유하고 이로 인해 한 화면에서 바꾼 정보가 다른 화면에 반영될 수 있다.

- 다른 클래스를 기반으로 하나의 클래스를 구축할 수 있다는 것은 Apple의 이전 UI 프레임워크인 UIKit에서는 매우 중요하지만 SwiftUI 앱에서는 훨씬 덜 사용된다. UIKit에서는 클래스 A가 클래스 B 위에 구축되고, 이 클래스가 클래스 C 위에 구축되고, 클래스 D가 클래스 D 위에 구축되는 식으로 긴 클래스 계층 구조를 갖는 것이 일반적이다.
- 멤버 단위 초기화가 없다는 것은 짜증나는 일이지만, 한 클래스가 다른 클래스를 기반으로 할 수 있다는 점을 고려하면 구현하기가 왜 까다로운지 알 수 있다. 만약 클래스 C가 추가 속성을 추가하면 C, B, A에 대한 모든 초기화가 중단될 것이다.
- 상수 클래스의 변수를 변경할 수 있다는 것은 클래스의 다중 복사 동작에 연결된다. 상수 클래스는 복사가 가리키는 포트를 변경할 수 없다는 것을 의미하지만 속성이 가변적이면 여전히 포트 내부의 데이터를 변경할 수 있다. 이는 구조체의 각 복사본이 고유하고 자체 데이터를 보유하는 구조체와 다르다.
- 클래스의 하나의 인스턴스가 여러 위치에서 참조될 수 있으므로 최종 복사본이 언제 파기되었는지 아는 것이 중요하다. 이것이 바로 초기화 해제 프로그램이 필요한 곳입니다. 이를 통해 마지막 복사본이 사라질 때 할당한 특수 리소스를 정리할 수 있다.

**==2. 어떻게 하나의 class가 다른 class를 계승하는가?==**

스위프트에서는 존재하는 class를 기반으로 class를 생성할 수 있으며, 이를 'inheritance(계승)'라고 부른다. 하나의 클래스가 다른 클래스를 기능적으로 계승할 때, 스위프트는 새로운 클래스에게 부모 클래스의 속성과 메서드에 대한 접근을 가능하게 한다. 이로 인해 작은 변화와 추가로 새로운 클래스를 커스텀할 수 있다.

계승하기 위해서는 child class의 이름 뒤에 콜론을 사용하고, 부모 클래스의 이름을 적는다. 아래는 하나의 속성과 초기화를 가진 Employee라는 클래스이다.

```swift
class Employee {
    let hours: Int

    init(hours: Int) {
        self.hours = hours
    }
}
```

우리는 Employee에 대해 hours 속성과 초기화를 가져오는 두 개의 서브클래스를 만들 수 있다. 

```swift
class Developer: Employee {
    func work() {
        print("I'm writing code for \(hours) hours.")
    }
}

class Manager: Employee {
    func work() {
        print("I'm going to meetings for \(hours) hours.")
    }
}
```

이 두 childclass가 어떻게 hours를 참조하고 있는지 보면, 굳이 반복해서 작성할 필요 없이, 속성이 추가된 것처럼 보인다.
이 클래스들은 Employee 클래스를 계승하지만, 자체적인 커스톰도 가능하다. 따라서 각각의 instance를 생성하고 work()를 호출하면, 각기 다른 결과를 얻을 수 있다.

```swift
let robert = Developer(hours: 8)
let joseph = Manager(hours: 10)
robert.work()
joseph.work()
```

속성을 공유하는 것처럼, 메소드도 공유할 수 있다. 예를 들어 아래 코드를 Employee 클래스에 추가해보자.

```swift
func printSummary() {
    print("I work \(hours) hours a day.")
}
```

Developer 클래스가 Employee 클래스를 계승하고 있기 때문에, 즉시 printSummary()를 Developer 의 Instance에서 호출할 수 있다.

```swift
let novall = Developer(hours: 8)
novall.printSummary()
```

계승한 메서드를 수정하고 싶다면 조금 복잡할 수 있다. 예를 들어 childclass에서 printSummary()를 조금 수정하고 싶을 수 있다.
만약 메서드를 child class에서 수정하고 싶다면, 재정의가 필요하다. 

- 재정의 없이 메서드를 수정하려고 하면, 코드가 build되지 않을 것이다.
- 재정의를 했는데, parent class의 메서드를 재정의한게 아니라면, 코드가 build되지 않을 것이다.

따라서 만약 Developers 클래스에 고유한 printSummary() 메서드를 만들고 싶다면, 디벨로퍼 클래스에 아래 내용을 추가하면 된다.

```swift
override func printSummary() {
    print("I'm a developer who will sometimes work \(hours) hours a day, but other times spend hours arguing about whether code should be indented using tabs or spaces.")
}
```

만약 parent class의 work()에 parameter가 필요하지 않은데 child class의 work()에는 parameter를 받고 있다면, override를 쓸 필요는 없다. 왜냐면 parent method를 대체하고 있는게 아니기 때문이다.

**==3. 어떻게 class에 초기화(initializer)를 추가하는가?==**

클래스의 iniitializer는 struct의 Initializer보다 복잡하다. 만약 child class가 어떤 커스텀 initializer라도 지니고 있다면, 속성 설정이 끝난 후 반드시 parent의 initializer를 호출해야 한다.

앞서 말했듯 클래스는 멤버 당 초기화를 제공하지 않는다. 이것은 계승과 관계 없이 무조건이다. 따라서 직접 initializer를 쓰거나, 모든 속성에 대한 기본값을 설정해야 한다.

```swift
class Vehicle {
    let isElectric: Bool

    init(isElectric: Bool) {
        self.isElectric = isElectric
    }
}
```

이 클래스는 하나의 Boolean 속성을 가지고 있고 속성값을 설정할 initializer를 지니고 있다. self를 여기서 사용하는 이유는 isElectric 파라미터를 같은 이름의 속성에 배정하기 위해서이다.

이제, Vehicle을 계승하는 Car 클래스를 만들어 보자.

```swift
class Car: Vehicle {
    let isConvertible: Bool

    init(isConvertible: Bool) {
        self.isConvertible = isConvertible
    }
}
```

하지만 이 코드는 작동이 안 될 것이다. Vehicle 클래스는 electric인지 아닌지에 대해 정보가 필요한데, 그 값을 안 줬기 때문이다.

따라서, Car 클래스를 만들때는 isElectric과 isConvertible에 대한 initializer가 모두 필요하다는 의미이다. 하지만 isElectric 값을 저장하는 것보다 패스하는게 낫다. super class에게 속한 initializer를 실행하도록 요청하자.

```swift
class Car: Vehicle {
    let isConvertible: Bool

    init(isElectric: Bool, isConvertible: Bool) {
        self.isConvertible = isConvertible
        super.init(isElectric: isElectric)
    }
}
```

super라는 값은 스위프트가 우리에게 자동적으로 제공하는 것이며, self와 유사하다. initializer처럼 parent class에 속한 method를 불러올 수 있게 해준다. 

따라서 우리는 Car class에 대한 인스턴스를 이렇게 만들 수 있다.

```swift
let teslaX = Car(isElectric: true, isConvertible: false)
```

**==4. 어떻게 클래스를 복사할까?**==

클래스 인스턴스의 모든 복사본은 같은 데이터를 공유한다. 한 복사본에서의 변화는 즉시 다른 복사본에 반영된다. 이를 이해하기 위해 아래 클래스를 보자.

```swift
class User {
    var username = "Anonymous"
}
```

이 클래스는 하나의 속성만 있다. 하지만 이것이 클래스 안에 저장되어 있기 때문에 클래스의 모든 복사본에 공유될 것이다.
따라서 이 클래스의 인스턴스를 이렇게 만들 수 있다.

```swift
var user1 = User()
```

그리고 user1의 복사본을 만들고 username 값을 변경할 수 있다.

```swift
var user2 = user1
user2.username = "Taylor"
```

그리고 이 값을 출력하면, 둘 다 Taylor를 출력한다.

```swift
print(user1.username)  
print(user2.username)
```

우리가 하나의 인스턴스만 변경했지만, 다른 인스턴스까지 변경된 것이다.
이것은 오류처럼 보일 수 있지만, 그저 하나의 특징이다. 매우 중요한 특징이기도 하다. 동일한 데이터를 앱 전체에서 공유되도록 할 수 있기 때문이다. SwiftUI에서는 클래스가 쉽게 공유될 수 있기 때문에 클래스에 데이터를 많이 의존한다.
반대로 Struct는 복사본 사이에서 데이터를 공유하지 않는다. 만약 우리가 class User를 struct User로 변경하면 print값에서 다른 결과를 얻게 된다. 원본에 영향을 미치지 않기 때문에, Taylor 대신 Anonymous를 출력할 것이다.
만약 당신이 클래스 인스턴스에 유일한 값을 넣고 싶다면(deep copy라고도 불린다) 새로운 인스턴스를 만들고 모든 데이터를 복사해야한다.

```swift
class User {
    var username = "Anonymous"

    func copy() -> User {
        let user = User()
        user.username = username
        return user
    }
}
```

이렇게 하면 copy()를 안전하게 호출하여 동일한 시작값의 객체를 얻을 수 있고, 어떤 변화도 원본에 영향을 미치지도 않을 것이다.

```swift
let original = User()
original.username = "Alice"

let copy = original.copy()
copy.username = "Bob"

print(original.username) // "Alice"
print(copy.username)     // "Bob"
```

**==5.어떻게 클래스에 deinitializer를 만드는가?==**

스위프트의 클래스는 선택적으로 deinitializer가 있을 수 있다. deinitializer는 객체가 파괴됐을 때 호출된다.

이것은 몇 가지 조건이 있다.
- initializer처럼, func를 함께 사용하지 않는다.
- 매개변수를 받거나 데이터를 반환하지 않는다. 따라서 괄호와도 함께 쓰이지 않는다.
- 클래스 인스턴스의 최종 복사본이 파괴되면 deinitializer는 자동적으로 호출된다.
- deinitializer는 직접 호출되지 않는다. 시스템에 의해 호출된다.
- structs는 deinitializer를 가지지 않는다.

언제 deinitializer가 호출되는지는 scope에 따라 결정된다. scope는 정보가 유효한 맥락을 의미한다.
- 함수 안에서 변수를 만들면 함수 밖에서는 접근할 수 없다.
- if 조건문 안에서 함수를 만들면 조건문 밖에서 쓸 수 없다.
- for 반복문에서 변수를 만들면 반복문 밖에서 쓸 수 없다.

함수, 반복문, 조건문에서는 늘 scope를 형성하기 위해 중괄호를 쓴다는 사실을 알 수 있다.
값이 범위를 벗어나면 해당 문맥이 사라짐을 의미한다. structs에서는 데이터가 파괴됨을 의미하지만, class에서는 그냥 하나의 데이터가 사라진 것이다. 다른 복사본들이 있을 수 있다. 하지만 최종 복사본이 사라지면(클래스 인스턴스를 가리키는 마지막 상수 혹은 변수) 기본 데이터도 파괴되고, 사용 중이던 메모리가 시스템으로 다시 반환된다.
이를 증명하기 위해 생성되거나 파괴됐을 때 메세지를 출력하는 클래스를 만들어보자.

```swift
class User {
    let id: Int

    init(id: Int) {
        self.id = id
        print("User \(id): I'm alive!")
    }

    deinit {
        print("User \(id): I'm dead!")
    }
}
```

이제 반복문을 통해 인스턴스를 파괴해보자. User 인스턴스를 루프 안에서 사용하면 반복이 끝날 때 파괴될 것이다.

```swift
for i in 1...3 {
    let user = User(id: i)
    print("User \(user.id): I'm in control!")
}
```

코드가 실행되면 각 유저마다 생성되고 파괴된 것을 알 수 있을 것이고, 다음 유저가 생성되기 전에 파괴된다는 것을 알 수 있을 것이다.
deinitializer는 클래스 인스턴스의 마지막 reference가 파괴될 때 호출된다. 
만약 우리가 User 인스턴스를 생성될 때마다 추가한다면, 배열이 모두 지워졌을 때 파괴될 것이다.

**==6. 어떻게 class 안의 변수를 활용하는가?==**

클래스는 같은 기본 데이터를 가리키는 표지같은 역할을 한다. 한 복사본에서의 변화가 다른 것들을 함께 변화시키기 때문에, 이는 중요하다. 또한 클래스가 변수 속성을 처리하는 방식 때문에 중요하기도 하다.

```swift
class User {
    var name = "Paul"
}

let user = User()
user.name = "Taylor"
print(user.name)
```

이는 상수 인스턴스 User를 만들고 값을 바꾼다. 상수의 값 자체(Paul -> Taylor)를 변화시킨다.
단, 상수값(let user = User())은 전혀 변경되지 않는다. 클래스 내부의 데이터는 변경되었지만 클래스 인스턴스 자체(우리가 만든 객체)는 변경되지 않았으며 실제로 상수로 만들었기 때문에 변경할 수 없다.

반대로, 만약 우리가 user 인스턴스와 name 속성을 모두 변수로 썼다면 어떻게 될까? 우리는 속성을 바꿀 수 있고, 또한 우리가 원하는 완전히 새로운 User 인스턴스도 바꿀 수 있다. (user = User()로 재정의 가능)

```swift
class User {
    var name = "Paul"
}

var user = User()
user.name = "Taylor"
user = User()
print(user.name)
```

이것은 Paul을 출력할 것이다. 왜냐면 우리가 name을 Taylor로 바꿨지만, 그 후에 전체 user 객체를 새로운 것으로 덮어쓰기 했고, 그러면서 Paul으로 값을 재설정했기 때문이다.

마지막 변형은 변수 인스턴스와 상수 속성을 갖는 것이다. 즉, 원하는 경우 새 User를 생성할 수 있지만 일단 완료되면 해당 속성을 변경할 수 없다.

따라서, 네 개의 선택지로 마무리된다.
- 상수 인스턴스, 상수 속성 - 항상 같은 이름을 지닌 user를 가리킨다.
- 상수 인스턴스, 변수 속성 - 같은 유저를 가리키지만, 이름은 바뀔 수 있다.
- 변수 인스턴스, 상수 속성 - 달느 유저를 가리키지만, 이름은 바뀌지 않는다.
- 변수 인스턴스, 변수 속성, 다른 이름을 지니고 이름이 바뀔 수 있다.

굉장히 헷갈리지만, 클래스 인스턴스가 공유되는 중요한 목적을 수반한다.
이는 structs와는 차이가 있다. 상수 structs는 속성이 변수이더라도 속성이 바뀔 수 없기 때문이다. 이를 바꾸려면 structs 자체를 수정해야 하는데, structs가 상수이기 때문에 이는 불가능하다.

이 모든 것의 장점은 클래스가 데이터를 변경하는 메서드에 mutating 키워드를 사용할 필요가 없다는 것이다. 이 키워드는 structs에 정말 중요하다. 왜냐하면 상수 structs는 생성 방법에 상관없이 속성을 변경할 수 없기 때문이다. 따라서 상수 structs 인스턴스에 변경 메서드를 호출하는 것은 허용되지 않는다.

