
# Swift 함수 학습 가이드

## 1. 함수 개요 (Functions Overview)

- **함수의 정의 및 목적**:
    - 함수는 코드를 **재사용**할 수 있도록 프로그램의 특정 코드 덩어리를 분리하고 이름을 부여하는 방식으로 사용됩니다.
    - 이를 통해 동일한 코드를 계속해서 반복적으로 사용할 수 있게 됩니다.
- **함수 작성 기본 구조**:
    - 모든 함수는 `func` **키워드**로 시작하며, 그 뒤에 함수의 이름이 옵니다.
    - 함수의 본문은 **중괄호 `{}`** 안에 위치합니다. 이는 조건문(`if`)이나 반복문(`for`, `while`)과 유사한 구조입니다.
```
// 아무 매개변수 없이 실행되며, 단순히 메시지를 출력하는 함수
func sayHello() {
    print("안녕하세요! 함수의 기본 구조입니다.")
}

// 함수 호출
sayHello() 
// 출력: 안녕하세요! 함수의 기본 구조입니다.
```
- **함수 매개변수 (Parameters)**:
    - 함수는 동작을 제어하기 위해 **매개변수**를 받을 수 있습니다.
    - 매개변수의 개수는 0개, 1개 또는 그 이상일 수 있습니다 (하지만 50개는 권장되지 않습니다).
    - 매개변수는 **이름**, **콜론(:)**, 그리고 **타입** 순서로 하나씩 나열하며, 여러 개일 경우 **쉼표(,)**로 구분합니다.
    - **커스텀 외부 매개변수 이름**을 사용하여 코드를 더 읽기 쉽게 만들거나, **밑줄(`_`)**을 사용하여 특정 매개변수의 외부 이름을 비활성화할 수도 있습니다.
```
//예제1 : 매개변수
// 이름을 받아서 인사하는 함수
func greet(name: String) {
    print("안녕하세요, \(name)님!")
}

greet(name: "에코")
// 출력: 안녕하세요, 에코님!


//예제2 : 매개변수 여러 개(쉼표로 구분)
// 두 숫자를 받아서 덧셈 결과를 출력하는 함수
func addNumbers(a: Int, b: Int) {
    let result = a + b
    print("결과: \(result)")
}

addNumbers(a: 3, b: 5)
// 출력: 결과: 8


//예제3 : 외부 매개변수 커스텀 + 외부 이름 생략
// 외부 매개변수 이름 커스터마이징
func sendMessage(to recipient: String, message: String) {
    print("\(recipient)에게 보낸 메시지: \(message)")
}

sendMessage(to: "에코", message: "안녕하세요~")
// 출력: 에코에게 보낸 메시지: 안녕하세요~

// 외부 매개변수 이름 생략하기
func multiply(_ a: Int, _ b: Int) -> Int {
    return a * b
}

let result = multiply(4, 6)
print("곱셈 결과: \(result)")
// 출력: 곱셈 결과: 24
```
- **함수 반환 값 (Return Values)**:
    - 함수는 필요에 따라 **값을 반환**할 수 있습니다.
    - 함수에서 **여러 개의 데이터를 반환**해야 할 경우, **튜플(tuple)**을 사용하는 것이 가장 좋은 방법입니다.
    - 튜플은 딕셔너리나 배열과 유사하지만, 여러 개의 **명명된 요소(named elements)**를 가지며, 그 **크기와 타입, 이름이 고정**되어 있다는 점에서 차이가 있습니다.
```
//예제1 : 하나의 값만 반환하는 함수
// 나이를 받아서 성인인지 판별하는 함수
func isAdult(age: Int) -> Bool {
    return age >= 20
}

// 함수 호출
let result = isAdult(age: 22)
print("성인인가요? \(result ? "네" : "아니요")")
// 출력: 성인인가요? 네


//예제2 : 여러 개의 값을 튜플로 반환하는 함수
// 이름과 나이를 받아서 튜플 형태로 반환하는 함수
func getUserInfo() -> (name: String, age: Int) {
    let name = "에코"
    let age = 30
    return (name, age)
}

// 함수 호출
let user = getUserInfo()
print("이름: \(user.name), 나이: \(user.age)")
// 출력: 이름: 에코, 나이: 30


//예제3 : 튜플 반환  + 조건 분기 사용
// 숫자를 나눌 때 0으로 나누는 경우를 처리하는 함수
func divide(_ a: Int, by b: Int) -> (result: Int?, error: String?) {
    if b == 0 {
        return (nil, "0으로 나눌 수 없습니다")
    } else {
        return (a / b, nil)
    }
}

let outcome = divide(10, by: 0)
if let value = outcome.result {
    print("나눈 결과: \(value)")
} else {
    print("에러: \(outcome.error!)")
}
// 출력: 에러: 0으로 나눌 수 없습니다
```
## 2. 매개변수 기본값 설정 (Providing Default Values for Parameters)

- **기본값 매개변수의 필요성**:
    - 함수에 매개변수를 추가하면 **커스터마이징 지점**을 만들어 필요에 따라 다른 데이터를 전달할 수 있게 됩니다.
    - 코드를 유연하게 유지하기 위해 이러한 커스터마이징 지점을 추가하는 것이 유용하지만, 때로는 대부분의 경우 **동일한 동작**을 원할 때가 많습니다.
    - **기본 매개변수**를 사용하면 함수를 호출하기 쉽게 만들어서, **공통적인 기본값**을 제공할 수 있습니다.

- **기본값 설정 방법**:
    - Swift는 함수 매개변수 중 하나 또는 **모두**에 기본값을 제공할 수 있도록 지원합니다.
    - 기본값을 설정하려면 매개변수 이름과 타입 정의 뒤에 **공백**을 두고 **등호(`=`)**와 **기본값**을 지정합니다. 예를 들어, `end: Int = 12` 와 같이 사용합니다.
- **실제 예시**:
    - `printTimesTables(for number: Int, end: Int = 12)` 함수에서 `end` 매개변수에 기본값 `12`를 설정하면, `printTimesTables(for: 8)`과 같이 `end` 값을 **지정하지 않고 호출**할 경우 자동으로 `12`가 사용됩니다. 물론 `printTimesTables(for: 5, end: 20)`와 같이 `end` 값을 **명시적으로 지정**하여 호출할 수도 있습니다.
    - 경로 찾기 함수 `findDirections(from: String, to: String, route: String = "fastest", avoidHighways: Bool = false)`는 `route`를 "fastest"로, `avoidHighways`를 `false`로 설정하는 **합리적인 기본값**을 가집니다. 이를 통해 `findDirections(from: "London", to: "Glasgow")`와 같이 더 짧은 코드로 호출할 수 있습니다.
    - `removeAll()` 함수에도 `keepingCapacity: Bool` 매개변수에 `false`라는 기본값이 있어, 배열 항목을 제거할 때 **메모리 용량을 유지할지 여부**를 선택할 수 있는 유연성을 제공합니다.
- **기본값 매개변수의 이점**:
    - 기본 매개변수를 사용하면 함수 호출 시 코드를 **더 짧고 간단하게** 만들면서도, 필요할 때 **유연성**을 유지할 수 있습니다.
    - Swift 개발자들이 매우 흔하게 사용하는 기능이며, 정기적으로 변경되어야 하는 **중요한 부분에 집중**할 수 있도록 돕고, 복잡한 함수를 **단순화**하며 코드를 작성하기 쉽게 만듭니다.
```
// 기본값을 여러 개 사용한 함수
func findDirections(from: String, to: String, route: String = "fastest", avoidHighways: Bool = false) {
    print("출발지: \(from), 도착지: \(to)")
    print("경로: \(route), 고속도로 우회: \(avoidHighways ? "예" : "아니요")")
}

// 기본값 사용
findDirections(from: "서울", to: "부산")

// 일부 기본값 덮어쓰기
findDirections(from: "서울", to: "부산", route: "scenic")

// 모든 매개변수 명시
findDirections(from: "서울", to: "부산", route: "shortest", avoidHighways: true) 
```

## 3. 함수에서 에러 처리 (Handling Errors in Functions)

- **에러 처리의 중요성**:
    - 파일이 없거나 네트워크가 끊기는 등 문제가 발생하는 것은 흔한 일입니다.
    - 이러한 에러를 **우아하게 처리하지 않으면** 앱이 **충돌(crash)**할 수 있습니다.
    - Swift는 개발자가 에러를 처리하거나 최소한 에러의 존재를 **인지하도록 강제**합니다. 에러 처리를 제대로 시도하지 않으면 코드가 **컴파일되지 않습니다**.
- **Swift 에러 처리의 세 단계**: Swift에서 에러를 처리하는 과정은 다음과 같은 **세 가지 핵심 단계**로 이루어집니다:
    1. **에러 정의**:
        - 코드에서 발생할 수 있는 모든 에러를 **열거형(enum)**으로 정의합니다. 이 열거형은 Swift의 내장 **`Error` 타입**을 기반으로 합니다.
        - 예를 들어, `enum PasswordError: Error { case short, obvious }`와 같이 비밀번호 관련 에러를 `short`와 `obvious`로 정의할 수 있습니다. 이들은 단지 가능한 에러의 존재를 의미합니다.
    2. **에러를 던지는 함수 작성**:
        - 심각한 문제가 발견되면 하나 이상의 정의된 에러를 **던질(throw)** 수 있는 함수를 작성합니다.
        - 에러가 "던져진다"는 것은 함수에서 **치명적인 문제**가 발생하여 정상적인 실행을 계속할 수 없고, 값을 반환하지 않고 **즉시 종료**되며, 에러가 다른 코드 블록에서 처리되도록 전달된다는 의미입니다.
        - 함수가 에러를 던질 수 있다면, 함수의 **반환 타입 앞에 `throws` 키워드**를 명시해야 합니다.
        - `throws` 키워드는 함수가 에러를 **던질 수 있음**을 의미하며, 반드시 에러를 던져야 한다는 의미는 아닙니다.
        - 에러를 던질 때는 `throw` 키워드 뒤에 정의된 에러 중 하나를 사용합니다 (예: `throw PasswordError.short`). 에러가 던져지면 함수는 **즉시 종료**되고, 이후의 코드는 실행되지 않습니다.
    3. **에러 처리**:
        - 함수를 실행하고 발생할 수 있는 모든 에러를 처리해야 합니다. 실제 Swift 프로젝트에서는 `do`, `try`, `catch` **세 가지 키워드**를 사용하여 에러를 처리합니다.
- **`do-try-catch` 블록**:
    - **`do` 블록**: 에러를 던질 수 있는 코드를 포함하는 **코드 블록**을 시작할 때 사용합니다.
    - **`try` 키워드**: `do` 블록 내에서 **던지는 함수**를 호출할 때 반드시 `try`를 붙여야 합니다.
        - **`try` 키워드의 중요성**: `try`는 일반적인 코드 실행이 **중단될 수 있음**을 개발자 자신과 다른 개발자들에게 **시각적으로 알리는 신호**입니다. Swift가 모든 던지는 함수 앞에 `try`를 강제하는 주된 이유는, 코드의 어느 부분이 에러를 발생시킬 수 있는지 **명확히 인지**하도록 하기 위함입니다. 예를 들어, 하나의 `do` 블록 내에 여러 함수 호출이 있을 때, `try`가 붙은 함수만 에러를 던질 수 있음을 명확히 보여줍니다.
        - **`try!` 사용 시 주의사항**: `try!`는 `do`나 `catch` 블록을 요구하지 않는 `try`의 다른 버전입니다. 하지만 `try!`를 사용한 함수에서 **에러가 던져지면 앱이 실제 충돌(fatal crash)**합니다. 따라서 에러가 발생하지 않을 것이라고 **절대적으로 확신할 때만** 드물게 사용해야 합니다.
    - **`catch` 블록**: `do` 블록 내에서 발생한 **모든 에러를 처리**합니다. `try`를 사용할 때는 반드시 `do` 블록 안에 있어야 하며, `catch` 블록에서 에러를 처리해야 합니다.
        - **특정 에러 캐치**: 모든 종류의 에러를 처리하는 **일반 `catch` 블록**은 항상 필요하지만, 원하는 경우 **특정 에러**를 명시하여 사용자 지정 메시지를 표시할 수 있습니다. 예를 들어, `catch PasswordError.short { ... }` 또는 `catch PasswordError.obvious { ... }`와 같이 특정 에러 `case`에 대한 처리를 분리할 수 있습니다. 마지막의 일반 `catch { ... }` 블록은 "포켓몬 캐치(Pokemon catch)"라고도 불리며, 모든 나머지 에러를 "잡아야" 하기 때문에 사용됩니다.
        - **에러 메시지**: Apple의 자체 프레임워크에서 던져지는 대부분의 에러는 사용자에게 표시할 수 있는 **의미 있는 메시지**를 제공합니다. Swift는 `catch` 블록 내에서 **`error` 상수**를 자동으로 제공하며, `error.localizedDescription`을 사용하여 발생한 일에 대한 일반적인 언어 설명을 읽는 것이 일반적입니다.
- **던지는 함수 사용 시기**:
    - 던지는 함수는 함수가 에러를 **처리할 수 없거나 처리할 의사가 없을 때** 사용됩니다. 이는 반드시 에러를 던진다는 의미가 아니라, **던질 가능성**이 있다는 의미입니다.
    - 에러 처리에는 여러 유효한 해결책이 있습니다: 에러를 함수 내에서 직접 처리하거나, 호출한 곳으로 에러를 **전파(error propagation)**하거나, 일부는 함수 내에서 처리하고 나머지는 전파하는 방식 등이 있습니다.
    - **초보자의 경우**, 처음에는 던지는 함수 사용을 **대부분 피하는 것**이 좋습니다. 왜냐하면 던지는 함수를 사용할 때마다 모든 에러를 처리해야 하므로 "전염성"이 강하게 느껴질 수 있고, 에러가 더 전파되면 "감염"이 확산되는 것처럼 느껴질 수 있기 때문입니다.
    - 점차적으로 에러 관리에 익숙해지면서 던지는 함수 사용에 자신감을 얻게 될 것입니다.

```
import SwiftUI

struct ContentView: View {
    @State private var username: String = ""
    @State private var password: String = ""
    @State private var loginMessage: String = ""

    // 1. 에러 정의
    enum LoginError: Error {
        case emptyUsername
        case shortPassword
        case wrongPassword
    }

    // 2. 에러를 던지는 함수
    func login(username: String, password: String) throws -> String {
        if username.isEmpty {
            throw LoginError.emptyUsername
        }
        if password.count < 6 {
            throw LoginError.shortPassword
        }
        if password != "123456" {
            throw LoginError.wrongPassword
        }
        return "로그인 성공!"
    }

    var body: some View {
        VStack(spacing: 20) {
            TextField("사용자 이름", text: $username)
                .textFieldStyle(RoundedBorderTextFieldStyle())
            SecureField("비밀번호", text: $password)
                .textFieldStyle(RoundedBorderTextFieldStyle())

            Button("로그인 시도") {
                do {
                    let result = try login(username: username, password: password)
                    loginMessage = result
                } catch LoginError.emptyUsername {
                    loginMessage = "⚠️ 사용자 이름을 입력해주세요."
                } catch LoginError.shortPassword {
                    loginMessage = "⚠️ 비밀번호가 너무 짧아요. 6자 이상 필요해요."
                } catch LoginError.wrongPassword {
                    loginMessage = "❌ 비밀번호가 틀렸어요."
                } catch {
                    loginMessage = "❗️예기치 못한 오류: \(error.localizedDescription)"
                }
            }
            .padding()
            .background(Color.blue)
            .foregroundColor(.white)
            .cornerRadius(8)
  
            Text(loginMessage)
                .foregroundColor(.red)
        }
        .padding()
    }
}
```