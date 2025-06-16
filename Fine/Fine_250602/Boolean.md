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