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

## 체크포인트 2

이 체크포인트는 배열, 딕셔너리, 세트를 학습한 후 배운 내용을 되짚어보기 위한 작은 코딩 과제입니다.

**과제**: 문자열 배열을 생성하고, 배열 내 **전체 항목 수**와 **고유 항목 수**를 출력하는 코드를 작성합니다.

**힌트**:

1. `let albums = ["Red", "Fearless"]`와 같이 문자열 배열을 생성합니다.
2. 배열의 전체 항목 수는 `albums.count`를 사용하여 얻을 수 있습니다.
3. `count`는 세트(sets)에도 존재합니다.
4. 배열로부터 `Set(someArray)`를 사용하여 세트를 만들 수 있습니다.
5. 세트는 중복 항목을 포함하지 않습니다.

---
>[!question]
>GQ1. GQ를 쓰세요
>GQ2. GQ를 쓰세요

## Description
- 개요와 설명을 작성

## 주요 기능
+ 실제 활용을 작성

## 코드 예시
+ 실제 코드 예시를 작성

## Keywords
+ 파생된 키워드들을 작성

## References
- 참고한 레퍼런스를 작성 (예 : Apple의 공식 문서)