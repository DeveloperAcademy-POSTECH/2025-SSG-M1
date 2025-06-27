# 1. [How to store truth with Booleans](https://www.hackingwithswift.com/quick-start/beginners/how-to-store-truth-with-booleans)

<<<<<<< Updated upstream
* **Boolean: true/false 연산자**
=======
* true/false 연산자
>>>>>>> Stashed changes
```swift
let goodDogs = true
let gameOver = false
```

```swift
let isMultiple = 120.isMultiple(of: 3)
```

* 다른 데이터 타입들과는 달리, Boolean은 사칙연산이 없음.
<<<<<<< Updated upstream
* !, 'not': true를 false로, false를 true로 바꿈.
=======
* ! 'not' 은 있음. true를 false로, false를 true로 바꿈.
>>>>>>> Stashed changes
```swift
var isAuthenticated = false
 isAuthenticated = !isAuthenticated
 print(isAuthenticated) // true
 isAuthenticated = !isAuthenticated
 print(isAuthenticated) // false
 ```

* toggle() = !
```swift
 var gameOver = false
 print(gameOver) // false

 gameOver.toggle()
 print(gameOver) // true
```
---
**Q.** Boolean을 소화하는 방식에는 어떤 것들이 있는지?
<<<<<<< Updated upstream
**A.** Boolen은 UI의 상태를 조건에 따라 제어할 때 자주 사용함.  
=======
A. Boolen은 UI의 상태를 조건에 따라 제어할 때 자주 사용함.  
>>>>>>> Stashed changes

**1. [@State](https://github.com/State)와 조건부 렌더링**
```swift
struct ContentView: View {
<<<<<<< Updated upstream
@State private var isOn = false        // @State는 Boolean을 저장하고 UI와 연결
=======
@State private var isOn = false          // @State는 Boolean을 저장하고 UI와 연결.
>>>>>>> Stashed changes

var body: some View {
    Toggle("Power", isOn: $isOn)

<<<<<<< Updated upstream
    if isOn {                         // if isOn으로 뷰의 표시 여부를 조건부로 결정
=======
    if isOn {                                            // if isOn으로 뷰의 표시 여부를 조건부로 결정.
>>>>>>> Stashed changes
        Text("System is ON")
    } else {
        Text("System is OFF")
        }
   }
}
```

**2. 뷰 Modifier에서 Boolean 활용**
```swift
struct ContentView: View {
@State private var isCritical = true

 var body: some View {
Text("Caution")
    .foregroundColor(isCritical ? .red : .primary)
    .bold(isCritical)
<<<<<<< Updated upstream
    ```
- Boolean 값을 통해 .foregroundColor, .bold() 등의 modifier를 동적으로 적용.
=======
    
- Boolean 값을 통해 .foregroundColor, .bold() 등의 modifier를 동적으로 적용.
```
>>>>>>> Stashed changes

**3. .opacity, .disabled, .hidden 같은 속성 제어**
```swift
struct ContentView: View {
 @State private var isFormValid = true

 func submit() {
  isFormValid.toggle()    // 버튼 누르면 true ↔ false 바뀜
 }
 var body: some View {
  Button("Submit", action: submit)
      .disabled(!isFormValid)
      .opacity(isFormValid ? 1.0 : 0.5)
 }
}
```
- Boolean 값에 따라 사용자의 상호작용을 제한하거나 시각적으로 처리.

**4. Binding을 이용한 하위 뷰와의 상태 공유**
```swift
struct ParentView: View {
    @State private var isPresented = false

    var body: some View {
        ChildView(isPresented: $isPresented)
    }
}

struct ChildView: View {
    @Binding var isPresented: Bool

    var body: some View {
        Toggle("Show modal", isOn: $isPresented)
    }
}
```
- [@binding](https://github.com/binding)은 상위 뷰의 Boolean 값을 하위 뷰에서 공유 및 조작 가능하게 해줌.

**5. 애니메이션 조건에 사용**
```swift
withAnimation {
    isExpanded.toggle()
}
```

**6. sheet, alert, popover 등에서 Boolean로 제어**
```swift
@State private var showSheet = false

var body: some View {
    Button("Show Sheet") {
        showSheet = true
    }
    .sheet(isPresented: $showSheet) {
        Text("This is a modal sheet")
    }
}
```
- isPresented: Binding은 sheet나 alert 등 표현 여부에 직접 사용됨.

**7. toggle() 메서드로 간결한 상태 전환**
```swift
Button("Toggle") {
    isActive.toggle()
}
```
---
**Q.** Boolean과 enum은 각각 어떤 때 사용하는가?
A. Boolean: 상태가 단순한 두 가지 값  
<<<<<<< Updated upstream
   enum: 상태가 단순한 두 가지 값 이상, enum이 더 명확하고 확장성이 큼.  
   예: enum AuthState { case loggedOut, loggedIn, loading }
   
=======
enum: 상태가 단순한 두 가지 값 이상, enum이 더 명확하고 확장성이 큼.  
예: enum AuthState { case loggedOut, loggedIn, loading }

>>>>>>> Stashed changes
---
**Q.** .toggle() 에서 () 안에 들어갈 수 있는 게 뭐가 있나요?
A. 아무 것도 올 수 없어요.  
.toggle()은 매개변수가 없는 메서드입니다.  
괄호 안에 값을 넣을 수 없고, 넣으면 컴파일 에러가 납니다.

<<<<<<< Updated upstream
=======
- [@State](https://github.com/State)나 [@binding](https://github.com/binding)인 Bool에 사용 가능
>>>>>>> Stashed changes
```swift
@State private var isOn = false

Button("Toggle") {
   isOn.toggle()  // true ↔︎ false 전환
}
```
<<<<<<< Updated upstream

- 옵셔널에는 직접 쓸 수 없어요
```swift
var maybeFlag: Bool? = true
maybeFlag?.toggle()     // ✅ OK (Optional Chaining => 값이 있으면 
/* 'toggle()' 실행, 값이 없으면 아무 일도 안 일어남 => "만약 maybeFlag 안에 값이 있다면 그 값을 바꿔줘"의 의미.) */
=======
- 옵셔널에는 직접 쓸 수 없어요
```swift
var maybeFlag: Bool? = true
maybeFlag?.toggle()     // ✅ OK (Optional Chaining => 값이 있으면 'toggle()' 실행, 값이 없으면 아무 일도 안 일어남 => "만약 maybeFlag 안에 값이 있다면 그 값을 바꿔줘"의 의미.)
>>>>>>> Stashed changes
maybeFlag.toggle()      // ❌ Error! Bool?엔 toggle() 없음
```

**Q.** 옵셔널에 쓰려면?
A. 옵셔널을 확실하게 풀어주면 돼요!

**✅ 방법 1: `if let(var)`으로 안전하게 꺼내기**
•	값이 있을 때만 꺼내서 바꾸고, 다시 넣어줌
•	값을 꺼내서 직접 처리하면, 더 복잡한 작업(예: 로그 찍기, 조건 확인 등)을 함께 할 수 있음.
```swift
if var unwrapped = maybeFlag {  // 1
    unwrapped.toggle()          // 2
    maybeFlag = unwrapped       // 3
}
```

1  
	• maybeFlag는 옵셔널 Bool로 값이 true, false, nil의 세 가지 중 하나.  
	• “만약 maybeFlag 안에 값이 있으면, 그걸 꺼내서 unwrapped라는 이름으로 써볼게!”  
	• 만약 maybeFlag가 nil이면? → 아래 코드는 아예 실행되지 않음!  
2  
	• unwrapped가 true 면 false로, false면 true로 값 변경.  
3  
	• unwrapped를 다시 maybeFlag로 변경. 원래 값인 maybeFlag가 진짜로 바뀌게 됨.

<<<<<<< Updated upstream
**✅ 방법 2: 옵셔널 체이닝 (?)**
=======
**✅ 방법 2: 옵셔널 체이닝 (?)**  
>>>>>>> Stashed changes
• 값이 있을 때만 알아서 바꿔줌  
• 제일 간단하고 안전함!
```swift
maybeFlag?.toggle()
```

**✅ 방법 3: 기본값을 줌**  
• 이건 값을 복사해서 바꾸는 거라 maybeFlag 자체는 바뀌지 않음.
```swift
<<<<<<< Updated upstream
(maybeFlag ?? false).toggle() // ❌ 이렇게 쓰면 바뀌는 건 복사본!  
```

**✨ 정리** 
| 코드 | 작동 방식 | 안전함? | 실제 변수 값이 바뀌나?  |
| maybeFlag?.toggle() | 값이 있을 때만 바꿈 | ✅ | ✅ | 
| maybeFlag.toggle() | 옵셔널엔 .toggle() 없음 (에러!) | ❌ | ❌ | 
| if let var ... | 값 꺼내서 바꾼 뒤 다시 넣음. | ✅ | ✅ | 
| (maybeFlag ?? false).toggle() | 복사된 값만 바뀜, 원본은 그대로 | ✅ |
=======
(maybeFlag ?? false).toggle() // ❌ 이렇게 쓰면 바뀌는 건 복사본!
```

**✨ 정리 ** 
코드 | 작동 방식 | 안전함? | 실제 변수 값이 바뀌나?  
maybeFlag?.toggle() | 값이 있을 때만 바꿈 | ✅ | ✅  
maybeFlag.toggle() | 옵셔널엔 .toggle() 없음 (에러!) | ❌ | ❌  
if let var ... | 값 꺼내서 바꾼 뒤 다시 넣음. | ✅ | ✅  
(maybeFlag ?? false).toggle() | 복사된 값만 바뀜, 원본은 그대로 | ✅
>>>>>>> Stashed changes
