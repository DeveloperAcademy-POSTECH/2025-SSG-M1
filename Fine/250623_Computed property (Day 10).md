# 2. [How to compute property values dynamically](https://www.hackingwithswift.com/quick-start/beginners/how-to-compute-property-values-dynamically)

## 동적으로 계산되는 프로퍼티(Computed Property)
* 프로퍼티(property): 클래스나 구조체(struct), 열거형(enum) 안에 있는 값(속성).
* 이 프로퍼티는 크게 두 가지로 나뉨.
	•	저장 프로퍼티(stored property): 값을 직접 저장하는 속성. 변수 또는 상수.
	•	계산 프로퍼티(computed property): 값을 저장하지 않고, 필요할 때마다 계산해서 돌려주는 속성. 저장 프로퍼티와 함수의 조합(저장 프로퍼티처럼 접근하지만 함수처럼 작동함).

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
vacationRemaining: 실제 할당된 휴가에서 실제 사용한 휴가를 뺀 값을 계산.

```swift
var archer = Employee(name: "Sterling Archer", vacationAllocated: 14)
archer.vacationTaken += 4
print(archer.vacationRemaining)
archer.vacationTaken += 4
print(archer.vacationRemaining)
```
* vacationRemaining을 읽을 수는 있지만 쓸 수는 없음. vacationRemaining은 “계산 프로퍼티(computed property)“로, 값을 직접 저장하지 않고, 매번 계산해서 보여줌.
   즉, 읽기(getter)는 가능하지만, 쓰기(setter)는 안 됨.

```swift
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
```swift
archer.vacationRemaining = 5 // 이렇게 직접 값을 넣으려고 하면 에러!
```
이렇게 쓸 수는 없음.
왜냐하면, “남은 휴가일수를 바꾼다”는 게 실제로 어떤 값을 바꿔야 하는지 Swift가 알 수 없기 때문.

### getter와 setter란?
	•	getter: 값을 읽을 때 실행되는 코드 (예: vacationRemaining을 읽을 때)
	•	setter: 값을 쓸 때 실행되는 코드 (예: vacationRemaining에 값을 넣으려고 할 때)

getter만 있으면 읽기 전용.
setter까지 있으면 읽고 쓸 수 있음.

#### vacationRemaining의 setter를 만들 때 고민할 점
만약 vacationRemaining에 값을 넣을 수 있게 하려면, setter를 만들어야 함.
그런데, vacationRemaining을 바꾼다는 건 실제로 어떤 값을 바꿔야 하나?
	•	vacationAllocated(할당된 휴가일수)를 바꿔야 할까?
	•	vacationTaken(사용한 휴가일수)를 바꿔야 할까?
예를 들어, vacationRemaining을 5로 바꾼다고 하면,
	•	할당된 휴가일수는 그대로 두고, 사용한 휴가일수를 바꿔서 남은 휴가가 5가 되게 할 수도 있고,
	•	혹은 사용한 휴가일수는 그대로 두고, 할당된 휴가일수를 바꿀 수도 있음.
이렇게 여러 가지 방법이 있기 때문에, setter를 직접 구현해줘야 Swift가 어떻게 해야 하는지 알 수 있음.

예) vacationTaken을 바꾸는 setter
아래처럼 setter를 만들어주면, vacationRemaining에 값을 넣을 수 있음.
```swift
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

### 정리
	•	vacationRemaining은 계산 프로퍼티이기 때문에, 기본적으로 읽기만 가능(getter만 있을 때).
	•	vacationRemaining에 값을 넣으려면, setter(쓰기용 코드)를 구현해야 함.
	•	setter를 만들 때는, 어떤 값을 바꿀지(휴가 할당량? 사용량?)를 직접 정해줘야 함.
	•	setter와 getter를 모두 구현하면, 읽고 쓰는 것이 모두 가능함.

-----
# Property

1. 프로퍼티란?
Swift에서 프로퍼티(property)는 구조체(struct)에 정보를 붙여주는 역할을 함.
예) 사람 정보를 담는 구조체가 있다면 이름(name), 나이(age) 같은 값이 프로퍼티.

2. 프로퍼티의 두 가지 종류
Swift에는 프로퍼티가 크게 두 가지가 있음.

(1) 저장 프로퍼티(stored property)
	•	값을 나중에 사용하기 위해 메모리에 저장해 둠.
	•	값을 바꿀 수도 있고, 읽을 수도 있음.
	•	예시:
```swift
struct User {
   var name: String // 저장 프로퍼티
   var age: Int     // 저장 프로퍼티
}
```

(2) 계산 프로퍼티(computed property)
	•	값을 직접 저장하지 않고, 호출될 때마다 다시 값을 계산함.
	•	실제로는 함수처럼 동작하지만, 프로퍼티처럼 사용.
	•	예시:
```swift
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
	•	값을 메모리에 저장해 두니까, 읽을 때마다 계산하지 않아 빠름.
	•	예: 이름, 나이, 이메일 주소 등
(2) 값이 다른 프로퍼티에 따라 계속 달라지는 경우 → 계산 프로퍼티
	•	항상 최신 상태를 반영해야 할 때 유용.
	•	예: 넓이(area)는 width와 height가 바뀌면 자동으로 바뀌어야 하니까 계산 프로퍼티가 좋음.
(3) 성능(퍼포먼스)도 고려해야 함
	•	저장 프로퍼티는 값을 한 번만 계산해서 저장하니, 자주 읽을 때 빠름.
	•	계산 프로퍼티는 읽을 때마다 계산하니, 자주 읽으면 느려질 수 있음.
	•	반대로, 거의 안 읽는 값이라면 굳이 저장하지 않고 계산 프로퍼티로 두는 게 메모리를 아낄 수 있음.
	
5. 의존성(dependency)도 중요한 기준
	•	어떤 프로퍼티가 다른 프로퍼티 값에 따라 달라진다면, 계산 프로퍼티로 만들어야 항상 최신 값을 얻을 수 있음.
	•	저장 프로퍼티로 만들면, 값이 바뀔 때마다 일일이 값을 새로 계산해서 저장해줘야 하니 번거롭고, 실수할 수 있음.
	
6. 추가 팁: lazy 프로퍼티와 프로퍼티 옵저버
	•	lazy 프로퍼티: 잘 안 쓰는 값을 저장 프로퍼티로 만들 때, 처음 사용할 때 한 번만 계산해서 저장해두는 방법. (메모리와 성능을 모두 챙길 수 있음)
	•	프로퍼티 옵저버: 저장 프로퍼티의 값이 바뀔 때마다 특정 코드를 실행할 수 있게 해줌. (의존성 문제를 어느 정도 해결)
	
7. 정리
	•	저장 프로퍼티: 값을 저장해두고, 자주 읽을 때 빠름.
	•	계산 프로퍼티: 값을 저장하지 않고, 읽을 때마다 계산해서 항상 최신 상태를 반영.
	•	선택 기준: 값이 자주 바뀌지 않고 자주 읽으면 저장 프로퍼티, 다른 값에 따라 달라지면 계산 프로퍼티.
	•	성능과 의존성도 고려해야 함.

## 계산 프로퍼티의 장점
	•	값이 바뀔 때마다 자동으로 최신 값을 계산할 수 있음.
	•	여러 저장 프로퍼티를 조합해서 새로운 값을 만들 수 있음.
	•	속성이 실제로 저장되지 않으니, 메모리도 절약할 수 있음.

## 중요 포인트 요약
	•	계산 프로퍼티는 값을 저장하지 않고, 필요할 때마다 코드를 실행해 값을 계산.
	•	읽기 전용(getter만) 또는 읽고 쓰기(getter + setter) 모두 가능함.
	•	계산 프로퍼티를 사용하면, 코드가 더 깔끔하고, 실시간으로 최신 값을 얻을 수 있음.