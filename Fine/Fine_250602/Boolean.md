# 1. [How to store truth with Booleans](https://www.hackingwithswift.com/quick-start/beginners/how-to-store-truth-with-booleans)
* true/false 연산자
```swift
let goodDogs = true
let gameOver = false
```

```swift
let isMultiple = 120.isMultiple(of: 3)
```

* 다른 데이터 타입들과는 달리, Boolean은 사칙연산이 없음.
* ! 'not' 은 있음. true를 false로, false를 true로 바꿈.
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

Q. Boolean을 소화하는 방식에는 어떤 것들이 있는지?
A. Boolen은 UI의 상태를 조건에 따라 제어할 때 자주 사용함.  
**1. [@State](https://github.com/State)와 조건부 렌더링**
struct ContentView: View {
@State private var isOn = false          // @State는 Boolean을 저장하고 UI와 연결.

var body: some View {
    Toggle("Power", isOn: $isOn)

    if isOn {                                            // if isOn으로 뷰의 표시 여부를 조건부로 결정.
        Text("System is ON")
    } else {
        Text("System is OFF")
        }
   }
}

**2. 뷰 Modifier에서 Boolean 활용**
struct ContentView: View {
@State private var isCritical = true

 var body: some View {
Text("Caution")
    .foregroundColor(isCritical ? .red : .primary)
    .bold(isCritical)
    
- Boolean 값을 통해 .foregroundColor, .bold() 등의 modifier를 동적으로 적용.

**3. .opacity, .disabled, .hidden 같은 속성 제어**
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
- Boolean 값에 따라 사용자의 상호작용을 제한하거나 시각적으로 처리.

**4. Binding을 이용한 하위 뷰와의 상태 공유**
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
- [@binding](https://github.com/binding)은 상위 뷰의 Boolean 값을 하위 뷰에서 공유 및 조작 가능하게 해줌.

**5. 애니메이션 조건에 사용**
withAnimation {
    isExpanded.toggle()
}

**6. sheet, alert, popover 등에서 Boolean로 제어**
@State private var showSheet = false

var body: some View {
    Button("Show Sheet") {
        showSheet = true
    }
    .sheet(isPresented: $showSheet) {
        Text("This is a modal sheet")
    }
}
- isPresented: Binding은 sheet나 alert 등 표현 여부에 직접 사용됨.

**7. toggle() 메서드로 간결한 상태 전환**
Button("Toggle") {
    isActive.toggle()
}

Q. Boolean과 enum은 각각 어떤 때 사용하는가?
A. Boolean: 상태가 단순한 두 가지 값  
enum: 상태가 단순한 두 가지 값 이상, enum이 더 명확하고 확장성이 큼.  
예: enum AuthState { case loggedOut, loggedIn, loading }