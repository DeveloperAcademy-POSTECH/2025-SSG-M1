클래스는 속성과 메서드를 갖는 기능을 포함하여 구조체와 많은 공통점을 가지고 있지만 클래스와 구조체 사이에는 5가지 주요 차이점이 있다.

**첫째, 클래스는 다른 클래스로부터 상속받을 수 있다. 즉, 상위 클래스의 속성과 메서드에 액세스할 수 있다. 원하는 경우 선택적으로 하위 클래스의 메서드를 재정의하거나 클래스를 최종 클래스로 표시하여 다른 사람이 하위 클래스로 분류하는 것을 막을 수 있다.

계승하기 위해서는 child class의 이름 뒤에 콜론을 사용하고, 부모 클래스의 이름을 적는다. 

```swift
class Employee {
    let hours: Int

    init(hours: Int) {
        self.hours = hours
    }
}

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

만약 메서드를 child class에서 수정하고 싶다면, 재정의가 필요하다. 

- 재정의 없이 메서드를 수정하려고 하면, 코드가 build되지 않을 것이다.
- 재정의를 했는데, parent class의 메서드를 재정의한게 아니라면, 코드가 build되지 않을 것이다.

따라서 만약 Developers 클래스에 고유한 printSummary() 메서드를 만들고 싶다면, 디벨로퍼 클래스에 아래 내용을 추가하면 된다.

```swift
override func printSummary() {
    print("I'm a developer who will sometimes work \(hours) hours a day, but other times spend hours arguing about whether code should be indented using tabs or spaces.")
}
```

**둘째, Swift는 클래스에 대한 멤버별 초기화를 생성하지 않으므로 직접 수행해야 한다. 하위 클래스에 자체 초기화 프로그램이 있는 경우 특정 시점에 항상 상위 클래스의 초기화 프로그램을 호출해야 한다.

직접 initializer를 쓰거나, 모든 속성에 대한 기본값을 설정해야 한다.

```swift
class Vehicle {
    let isElectric: Bool

    init(isElectric: Bool) {
        self.isElectric = isElectric
    }
}
```

이때 하위 클래스로 Car 클래스를 만든다면 상위 클래스의 멤버인 isElectric과 Car 클래스의 멤버인 isConvertible에 대한 initializer가 모두 필요하다. 하지만 isElectric 값은 super class에게 속한 initializer를 실행하도록 요청하자.

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

**셋째, 클래스 인스턴스를 만든 다음 복사본을 가져오면 모든 복사본이 동일한 인스턴스를 가리킨다. 이는 복사본 중 하나에서 일부 데이터를 변경하면 모두 변경된다는 의미이다.

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

아래 user1, user2는 같은 인스턴스를 가리킨다. 그리고 이 값을 출력하면, 둘 다 Taylor를 출력한다.

```swift
var user1 = User()
var user2 = user1
user2.username = "Taylor"
print(user1.username)  
print(user2.username)
```

그러나 아래와 같이 copy() 메서드를 활용하면 인스턴스의 값을 바꾸지 않고 변경이 가능하다.

```swift
let original = User()
original.username = "Alice"

let copy = original.copy()
copy.username = "Bob"

print(original.username) // "Alice"
print(copy.username)     // "Bob"
```

**넷째, 클래스에는 한 인스턴스의 마지막 복사본이 파괴될 때 실행되는 초기화 해제 프로그램이 있을 수 있다.

deinitializer는 객체가 파괴됐을 때 호출된다. 함수, if 조건문, for 반복문 안에서 선언된 변수는 범위를 벗어나면 파괴된다.

deinitializer에는 몇 가지 조건이 있다.
- initializer처럼, func를 함께 사용하지 않는다.
- 매개변수를 받거나 데이터를 반환하지 않는다. 따라서 괄호와도 함께 쓰이지 않는다.
- 클래스 인스턴스의 최종 복사본이 파괴되면 deinitializer는 자동적으로 호출된다.
- deinitializer는 직접 호출되지 않는다. 시스템에 의해 호출된다.
- structs는 deinitializer를 가지지 않는다.

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

실제 출력 예시:

User 1: I'm alive!
User 1: I'm in control!
User 1: I'm dead!
User 2: I'm alive!
User 2: I'm in control!
User 2: I'm dead!
User 3: I'm alive!
User 3: I'm in control!
User 3: I'm dead!

**마지막으로, 클래스 인스턴스 내부의 변수 속성은 인스턴스 자체가 변수로 생성되었는지 여부에 관계없이 변경될 수 있다.

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