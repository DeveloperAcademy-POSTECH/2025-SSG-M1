# Swift 복합 데이터 유형 및 타입 어노테이션

이 문서는 Swift 학습 과정에서 복합 데이터 유형 (배열, 딕셔너리, 세트, 열거형)과 타입 어노테이션에 대해 배운 내용을 정리합니다.

## 복합 데이터 유형 요약

Swift는 다양한 종류의 데이터를 다루기 위해 복합 데이터 유형을 제공합니다. 단순 데이터 유형을 넘어 여러 값을 함께 묶거나 사용자 정의 유형을 생성할 수 있습니다.

- **배열 (Arrays)**: 여러 값을 한 곳에 저장하며, 정수 인덱스를 사용하여 값을 읽어옵니다. 배열은 반드시 특정 타입을 포함하도록 전문화(specialized)되어야 합니다 (예: `[String]` 문자열 배열). `count`, `append()`, `contains()`와 같은 유용한 기능이 있습니다. 배열은 딕셔너리, 세트에 비해 **가장 자주 사용되는** 유형입니다.
- **딕셔너리 (Dictionaries)**: 여러 값을 저장하지만, 사용자가 지정하는 키를 사용하여 값을 읽어옵니다. 키와 값 모두 특정 타입을 갖도록 전문화되어야 합니다 (예: `[String: Int]` 문자열 키와 정수 값의 딕셔너리). 배열과 유사하게 `contains()`, `count`와 같은 기능이 있습니다. 배열 다음으로 자주 사용됩니다.
- **세트 (Sets)**: 여러 값을 저장하는 **세 번째 방법**이며, 저장 순서를 사용자가 선택할 수 없습니다. 특정 항목을 포함하는지 확인하는 데 매우 효율적입니다. 세트도 특정 타입을 포함하도록 전문화되어야 합니다 (예: `Set<String>` 문자열 세트). 세트는 배열, 딕셔너리에 비해 사용 빈도가 낮지만, 필요할 때 유용합니다.
- **열거형 (Enums)**: Swift에서 **사용자 정의 간단한 타입**을 생성할 수 있게 해줍니다. 이를 통해 허용 가능한 값의 범위를 지정할 수 있습니다 (예: 요일 목록, UI 테마 종류, 앱의 화면 종류 등). 열거형 값은 해당 열거형 자체와 동일한 타입을 갖습니다.

## 타입 어노테이션 사용 방법

Swift는 변수나 상수에 할당하는 값을 기반으로 데이터 타입을 자동으로 파악합니다. 이를 **타입 추론 (Type Inference)**이라고 합니다.

```
let surname = "Lasso" // Swift infers String
var score = 0       // Swift infers Int
```

하지만 때로는 값을 즉시 할당하고 싶지 않거나, Swift의 타입 추론 결과를 변경하고 싶을 때 **타입 어노테이션 (Type Annotation)**을 사용합니다.

타입 어노테이션은 변수/상수 이름 뒤에 콜론(:)을 붙이고 타입을 명시하는 방식입니다.

```
let surname: String = "Lasso" // Explicitly a String
var score: Int = 0         // Explicitly an Int
```

Swift가 추론하는 타입과 동일하게 명시하는 경우도 있지만, 다른 타입을 지정할 수도 있습니다. 예를 들어, 점수에 소수점이 필요하다면 `Int` 대신 `Double`로 명시할 수 있습니다.

```
var score: Double = 0 // Override inference to Double
```

타입 어노테이션이 필요한 주요 상황은 세 가지입니다:

1. **Swift가 타입을 스스로 파악할 수 없는 경우**. 이는 주로 초기 값이 할당되지 않은 상수에 발생합니다.
    
```
    let username: String // Must specify String as no initial value
    // ... complex logic ...
    username = "@twostraws" // Assign value later
```
    
    (`username`은 한 번만 값을 할당받아야 상수로 유지됩니다).
2. **Swift의 기본 추론 타입을 변경하고 싶은 경우**. (예: `0`을 `Int` 대신 `Double`로 취급하고 싶을 때 `var score: Double = 0`).
3. **값을 나중에 할당하고 싶은 경우**. 변수나 상수가 존재할 것임을 미리 알리지만 값을 바로 설정하지 않을 때 사용합니다.

```
var name: String // Declare exists, assign later
```

**빈 컬렉션 (배열, 딕셔너리, 세트) 생성 시**: 초기 값이 없으므로 타입 어노테이션이 필요할 수 있습니다. 빈 컬렉션은 데이터를 미리 모두 알지 못하고 나중에 추가해야 할 때 유용합니다.

```
var teams: [String] = [String]() // Empty array of Strings (explicit type annotation)
var clues = [String]()           // Empty array of Strings (type inference, but needs type definition on right side)
var cities: [String] = []        // Empty array of Strings (type annotation with empty literal)
```

타입 추론과 타입 어노테이션 중 무엇을 사용할지는 **개인의 스타일** 문제입니다. 소스 개발자는 코드를 더 짧고 읽기 쉽게 만들고, 초기 값 변경만으로 타입 변경이 가능하기 때문에 **타입 추론을 선호**한다고 합니다. 하지만 명시적인 타입 어노테이션을 항상 사용하는 것도 괜찮습니다.

**골든 룰**: Swift는 항상 변수와 상수에 포함된 데이터의 타입을 알고 있어야 합니다. 이것이 Swift가 타입 세이프(Type-Safe) 언어인 핵심이며, `5 + true`와 같은 부적절한 연산을 방지합니다. 타입 어노테이션으로 타입을 지정해도, 실제로 해당 값을 그 타입으로 변환하는 것이 **가능해야** 합니다 (`let score: Int = "Zero"` 와 같은 코드는 허용되지 않습니다).


### **GQ**
+ 1. 왜 애플은 타입 추론을 권장할까?(자랑일까?)
+ 2. Swift에서 타입을 추론할 때 어떤 것을 상위로 사용을 할까?
+ 3. 옵셔널은 무엇인가?
+ 4. Swift에서 사용하는 코어 데이터와 스위프트 데이터에 대해서 알아보고, 여기서 옵셔널을 사용하는 이유는 무엇인가?

## 1️⃣ 왜 애플은 타입 추론을 권장할까? (자랑일까?)

### ✅ 원인과 이유

- **가독성 향상**  
  Swift는 *간결하고 읽기 쉬운 코드*를 지향함.  
  → 타입을 명시하지 않고도 변수/상수 선언 가능 → 코드 간결

- **컴파일 타임 안전성** (컴파일 : 코드를 기계어로 바꾸는 작업) 
  타입은 **컴파일 시점에 정확하게 추론**됨 → 런타임 타입 오류 방지  
  → Swift는 "타입 안전성(type-safety)"을 매우 중요하게 생각함


- **현대적 언어 철학**  (가독성, 타입 안전성, 생산성, 유지보수성)
  Swift는 *Modern programming language*로서 **타입 추론**을 핵심 기능으로 제공  
  → WWDC에서는 Swift를 Fast(빠름), Modern(현대적임), Safe(안전함), Interactive(빠르게 실험 가능)라 말함.

### ✅ Swift 코드 예시

```swift
let message = "Hello, Echo!"  // String으로 추론
let count = 42                // Int로 추론
let ratio = 3.14              // Double로 추론
````

### ✅ 출처

[Swift Language Guide - The Basics](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/thebasics/#Type-Annotations)  
_"Swift uses type inference to work out the appropriate type."_

---

## 2️⃣ Swift에서 타입을 추론할 때 어떤 것을 상위로 사용할까?

### ✅ 원인과 이유

- **가장 구체적인 타입(specific type)** 으로 추론하려고 함.
    
- 여러 타입의 상위 타입이 필요한 경우 → **공통 상위(super) 타입 또는 프로토콜 타입**으로 추론
    

#### 우선순위

1️⃣ 리터럴 → 기본 타입 사용 (Int, Double, String 등)  
2️⃣ 컬렉션 → 가장 구체적인 타입 사용  
3️⃣ 다형성 상황 → 상위 클래스 또는 프로토콜 타입 사용

### ✅ Swift 코드 예시

```swift
// 1️⃣ 리터럴 → 기본 타입
let integer = 100     // Int
let pi = 3.1415       // Double

// 2️⃣ 컬렉션 → 구체적 타입
let fruits = ["Apple", "Banana", "Cherry"]  // [String]
```

### ✅ 리터럴 종류

| 리터럴 종류                        | 타입 후보들                              | Swift 기본 추론 타입                                      | 왜 그렇게 되는가                               |
| ----------------------------- | ----------------------------------- | --------------------------------------------------- | --------------------------------------- |
| 정수 리터럴 (e.g. `42`)            | Int, UInt, Int8~Int64               | **Int**                                             | 플랫폼 최적화 + 대부분 Int 사용                    |
| 소수 리터럴 (e.g. `3.14`)          | Double, Float, CGFloat              | **Double**                                          | 더 높은 정밀도, 안전성 우선                        |
| 문자열 리터럴 (e.g. `"Echo"`)       | String, NSString                    | **String**                                          | Swift의 기본 문자열 타입                        |
| 문자 리터럴 (e.g. `"E"`)           | String, Character                   | **String** ← 문자열로 인식 (따옴표 사용 시) / `'E'` → Character | Swift에서 `" "`는 String, `' '`는 Character |
| Boolean 리터럴 (`true`, `false`) | Bool                                | **Bool**                                            | 불리언은 Bool로 고정                           |
| 배열 리터럴 (`[1, 2, 3]`)          | [Int], [Double], [Any] 등            | **가장 구체적 타입 사용**                                    | 배열 요소의 타입을 보고 추론                        |
| 딕셔너리 리터럴 (`["a": 1, "b": 2]`) | [String: Int], [AnyHashable: Any] 등 | **가장 구체적 타입 사용**                                    | 키, 값의 타입을 보고 추론                         |

### ✅ 출처

[Swift Language Guide - Type Inference](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/thebasics/#Type-Inference)  
_"Swift always chooses the smallest possible type that can hold the literal value."_

---

# Any vs AnyObject vs AnyHashable 차이

## 🏷️ Any

### ✅ 의미
- **모든 타입을 담을 수 있음** → Swift의 *가장 상위 타입*

### ✅ 설명
- Value type(값 타입) + Reference type(참조 타입) 전부 담을 수 있음
- struct, class, enum, Int, String, Double, UIView 등 모두 가능

### ✅ 예시

```swift
let anyValue1: Any = 42        // Int
let anyValue2: Any = "Echo"    // String
let anyValue3: Any = [1, 2, 3] // Array<Int>
````

### ✅ 특징

- **정말 모든 것**을 담을 수 있음
    
- 하지만 꺼낼 때는 **타입캐스팅 필요** (as?, as!)

# Any에서 타입캐스팅 (as?, as!) 사용법

---

## 📌 기본 개념

- **Any는 모든 타입을 담을 수 있지만 → 꺼낼 때는 반드시 원래 타입으로 변환(캐스팅) 해야 사용 가능하다.**
- 그렇지 않으면 Swift는 타입이 뭔지 몰라서 연산도 못 하고 접근도 못 한다.

## 타입캐스팅 방법

| 키워드 | 설명 |
|--------|------|
| `as?`  | **Optional 타입으로 안전하게 캐스팅** → 실패 시 nil 반환 |
| `as!`  | **강제 캐스팅** → 실패 시 런타임 에러 발생 |

## 📌 예시 1️⃣ `as?` (안전한 캐스팅)

```swift
let anyValue: Any = "Echo"

// 안전한 캐스팅 → Optional(String) 반환
if let stringValue = anyValue as? String {
    print("String value:", stringValue)
} else {
    print("Casting failed")
}
````

### 출력 결과

```
String value: Echo
```

### 설명

- `as? String` → 성공하면 `stringValue`에 String이 들어감.
    
- 실패하면 `nil` → else 블록 실행됨 → **안전하게 처리 가능**.
    

## 📌 예시 2️⃣ `as!` (강제 캐스팅)

```swift
let anyValue: Any = "Echo"

// 강제 캐스팅 → 실패 시 런타임 에러 발생
let stringValue = anyValue as! String
print("String value:", stringValue)
```

### 출력 결과

```
String value: Echo
```

### 만약 잘못된 캐스팅을 하면?

```swift
let anyValue: Any = 42
let stringValue = anyValue as! String  // 런타임 크래시 발생 ❌
```

### 에러

```
Could not cast value of type 'Int' to 'String'
```

## 정리

|방법|사용 상황|안전성|
|---|---|---|
|`as?`|안전하게 시도 (옵셔널 반환)|✅ 안전|
|`as!`|타입이 확실할 때 강제로 캐스팅|⚠️ 위험 (잘못 쓰면 런타임 크래시 발생)|

---

## 🏷️ AnyObject

### ✅ 의미

- **모든 클래스 타입의 인스턴스**만 담을 수 있음 → Reference type 전용
    

### ✅ 설명

- 클래스는 Reference type → 그 인스턴스만 담을 수 있음
    
- struct, enum 같은 Value type은 담을 수 없음
    

### ✅ 예시

```swift
class MyClass {}
struct MyStruct {}

let objectValue: AnyObject = MyClass()  // 가능
// let objectValue2: AnyObject = MyStruct()  // 오류 발생! Value type은 안됨
```

### ✅ 특징

- **클래스 타입 인스턴스만 허용**
    
- 주로 Objective-C API와 연동할 때 많이 사용됨 (`NSObject` 기반 API들)
    

---

## 🏷️ AnyHashable

### ✅ 의미

- **Hashable 프로토콜을 따르는 값만 담을 수 있는 래퍼 타입**
    

### ✅ 설명

- Swift에서 Set의 요소, Dictionary의 Key는 반드시 Hashable 이어야 함
    
- AnyHashable은 서로 다른 타입의 Hashable 값을 하나로 담아서 처리할 때 사용
    

### ✅ 예시

```swift
let hashableValue1: AnyHashable = 42      // Int는 Hashable
let hashableValue2: AnyHashable = "Echo"  // String은 Hashable
let hashableValue3: AnyHashable = true    // Bool도 Hashable

let hashableSet: Set<AnyHashable> = [42, "Echo", true]
```

### ✅ 특징

- 오직 **Hashable 프로토콜을 따르는 값만 허용**
    
- 내부적으로 HashValue 를 기반으로 구분 가능
    
- Dictionary의 Key에 사용 가능
    

---

## 🎁 총정리 테이블

|타입|담을 수 있는 값|주요 용도|비고|
|---|---|---|---|
|**Any**|모든 타입 (Value + Reference)|타입이 다양한 값 다루기|가장 범용적|
|**AnyObject**|클래스 인스턴스만 (Reference type만)|Objective-C API 연동, 클래스 타입 전용|Value type 안 됨|
|**AnyHashable**|Hashable 프로토콜 채택 타입|Set 요소, Dictionary Key 등 Hash 기반 자료구조에 사용|Hashable 필수|

---

## 💡 언제 쓰나?

- **Any** → 정말 타입을 모를 때 (최후의 수단으로 사용 권장)
    
- **AnyObject** → 클래스만 받을 때 (ex. UIKit API에서 delegate 배열 등에 사용)
    
- **AnyHashable** → Dictionary Key에 여러 타입 섞어서 쓰고 싶을 때
    

---

## 📚 공식 문서 출처

- [Swift Language Guide - Any, AnyObject](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/thebasics/#Any-and-AnyObject)
    
- [AnyHashable Documentation](https://developer.apple.com/documentation/swift/anyhashable)
    

> _"Any can represent an instance of any type at all, including function types and optional types."_  
> _"AnyObject can represent an instance of any class type."_  
> _"AnyHashable is a type-erased hashable value."_

---

## ✨ 결론

- **Any** → 모든 것 (Value + Reference)
    
- **AnyObject** → Reference type (class) 전용
    
- **AnyHashable** → Hashable만 가능 → Set, Dictionary Key 등에서 사용
    

---

## 3️⃣ 옵셔널(Optional)은 무엇인가?

### ✅ 원인과 이유

- **nil(없음)** 을 안전하게 표현하기 위한 타입
    
- Swift는 null pointer dereference 오류를 방지하기 위해 → 옵셔널이라는 타입 제공
    
- 옵셔널은 "값이 있을 수도 있고 없을 수도 있음"을 **명시적**으로 표현하도록 강제  
    → Swift의 주요한 **안정성(safety)** 기능 중 하나
    

### ✅ Swift 코드 예시

```swift
var name: String? = "Echo"  // 옵셔널 String → 값이 있을 수도, 없을 수도 있음

// 옵셔널 바인딩
if let unwrappedName = name {
    print("Hello, \(unwrappedName)")
} else {
    print("No name provided")
}

// nil 할당 가능
name = nil
```

### ✅ 출처

[Swift Language Guide - Optionals](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/thebasics/#Optionals)  
_"You use optionals in situations where a value may be absent."_

---

## 4️⃣ Core Data 와 SwiftData → 옵셔널 사용하는 이유는?

### ✅ Core Data vs SwiftData

|Core Data|SwiftData|
|---|---|
|오래된 ORM (Objective-C 기반 설계)|Swift 전용 최신 ORM (2023 WWDC에서 소개됨)|
|`NSManagedObject` 기반|`@Model` 속성 기반, 코드가 더 간결|
|코드가 복잡|코드가 깔끔하고 Swift 친화적|

### ✅ 옵셔널 사용하는 이유

- **DB 설계에서 null(없음) 가능성 존재**  
    → Swift에서 이를 정확하게 표현하기 위해 옵셔널 사용
    
- **모든 값이 필수는 아님**  
    → 사용자 입력값, 서버 데이터 등에서 nil 가능성이 높음  
    → 옵셔널로 안전하게 표현 → 앱 크래시 방지
    

### ✅ SwiftData 코드 예시

```swift
import SwiftData

@Model
class User {
    var name: String
    var email: String?   // 옵셔널 사용 → 이메일 없는 사용자도 허용
    var age: Int
    
    init(name: String, email: String?, age: Int) {
        self.name = name
        self.email = email
        self.age = age
    }
}

let user1 = User(name: "Echo", email: "echo@example.com", age: 30)
let user2 = User(name: "NoEmailUser", email: nil, age: 25)  // email 옵셔널 활용
```

### ✅ 출처

- [SwiftData Documentation](https://developer.apple.com/documentation/swiftdata/)
    
- [Core Data Programming Guide - Optional Properties](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/CoreData/Articles/cdDesignTechniques.html#//apple_ref/doc/uid/TP40004399-SW7)  
    _"Optional attributes map to optional properties in your NSManagedObject subclasses."_
    

---

# 📚 총 정리

|항목|핵심 포인트|공식문서 출처|
|---|---|---|
|타입 추론 권장 이유|가독성 + 타입 안전성 유지|[Swift Language Guide - The Basics](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/thebasics/)|
|타입 추론 시 상위 타입 사용|기본적으로 가장 구체적 타입 사용, 필요시 상위 타입 사용|[Swift Language Guide - Type Inference](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/thebasics/#Type-Inference)|
|옵셔널이란?|nil 안정성 확보 (값이 있을 수도, 없을 수도 있음)|[Swift Language Guide - Optionals](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/thebasics/#Optionals)|
|Core Data / SwiftData에서 옵셔널 사용하는 이유|DB에서 nullable 필드 표현|[SwiftData Docs](https://developer.apple.com/documentation/swiftdata/), [Core Data Programming Guide](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/CoreData/Articles/cdDesignTechniques.html#//apple_ref/doc/uid/TP40004399-SW7)|
