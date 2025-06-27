# [Why do we need to mark some methods as mutating?](https://www.hackingwithswift.com/quick-start/understanding-swift/why-do-we-need-to-mark-some-methods-as-mutating)
구조체의 속성을 수정하는 것은 해당 구조체가 변수로 생성된 경우에만 가능함. 
구조체 _내부에서는_ 변수 구조체를 사용할지 상수 구조체를 사용할지 알 수 없으므로, Swift에는 구조체의 메서드가 속성을 변경하려고 할 때마다 해당 메서드를 `mutating` 마크 처리를 해줘야 함.

•	struct의 속성을 바꾸는 메서드는 반드시 mutating을 붙여야 한다.
•	mutating이 붙은 메서드는 let struct에서는 쓸 수 없다.
•	mutating이 붙었다고 하면, 실제로 안 바꿔도 Swift는 “바꾼다”고 믿는다.
•	mutating이 아닌 메서드에서는 mutating 메서드를 부를 수 없다.

```swift
struct User {
    var name: String
}

var user1 = User(name: "Tom") // 변수로 만든 struct
let user2 = User(name: "Amy") // 상수로 만든 struct

user1.name = "Jerry" // 가능!
user2.name = "Bob"   // 에러! (상수라서 못 바꿈)
```

## struct 안에서 속성 바꾸는 메서드 만들기
struct 안에 메서드(함수)를 만들 때, 그 메서드가 속성을 바꾸려고 하면 특별히 표시해줘야 함. 이걸 mutating이라고 함.
## 왜 mutating을 써야 할까?
struct 안에서 메서드를 만들 때, 그 메서드가 속성을 바꿀지 아닐지 컴파일러가 알아야 하므로 속성을 바꾸는 메서드는 반드시 mutating 키워드를 붙여야 함.

```swift
struct User {
    var name: String

    mutating func changeName(newName: String) {
        name = newName
    }
}
```
이렇게 mutating을 붙이면, Swift는 “이 메서드는 struct의 속성을 바꾼다”고 이해.
## mutating의 효과
1.	상수(let)로 만든 struct에서는 mutating 메서드를 쓸 수 없음
	•	let으로 만든 struct는 못 바꾸니까, mutating 메서드도 못 씀.
	•	var로 만든 struct만 mutating 메서드 사용 가능!
	
2.	mutating이 붙은 메서드는 실제로 속성을 안 바꿔도, Swift는 바꾼다고 생각함
	•	예를 들어, 아래처럼 실제로 아무 것도 안 해도, mutating이 붙어 있으면 let struct에서는 호출 못 함.
```swift
	mutating func doNothing() {
    // 아무 것도 안 함
}
```

3.	mutating이 안 붙은 메서드는 mutating 메서드를 호출할 수 없음
	•	만약 메서드A가 mutating이고, 메서드B가 mutating이 아니면, 메서드B 안에서 메서드A를 부를 수 없음.
	•	둘 다 mutating이어야 서로 호출할 수 있음.