# 1. [How to store truth with Booleans](https://www.hackingwithswift.com/quick-start/beginners/how-to-store-truth-with-booleans)

true/false 연산자
```swift
let goodDogs = true
let gameOver = false
```

```swift
let isMultiple = 120.isMultiple(of: 3)
```

다른 데이터 타입들과는 달리, Boolean은 사칙연산이 없음.
! 'not' 은 있음. true를 false로, false를 true로 바꿈.

```swift
var isAuthenticated = false
isAuthenticated = !isAuthenticated
print(isAuthenticated) // true
isAuthenticated = !isAuthenticated
print(isAuthenticated) // false
```

toggle() = !
```swift
var gameOver = false
print(gameOver) // false

gameOver.toggle()
print(gameOver) // true
```

# 2. [How to join strings together](https://www.hackingwithswift.com/quick-start/beginners/how-to-join-strings-together)

"+" 기호를 사용하거나 string interpolation(문자보간) 사용 
1) + 기호 사용
```swift
let firstPart = "Hello, "
let secondPart = "world!"
let greeting = firstPart + secondPart
``` // Hello, world!

```swift
let people = "Haters"
let action = "hate"
let lyric = people + " gonna " + action
print(lyric)
```
operator overloading: 한 operator가 어떻게 사용되는가에 따라 다른 의미를 갖는 것.
예) +: string + string => string 연결
정수나, 소수에서 사용되면 값을 더함.

"+" 기호 사용은 비효율적
```swift
let luggageCode = "1" + "2" + "3" + "4" + "5"
```
한 번에 12345로 가지 못함.
"1" + "2" => "12" + "3" => "123" + "4" => "1234" + "5" => "12345"
코드가 끝날 때까지 12, 123, 1234를 모두 가지고 있음 (사용되지 않는데도).

2) string interpolation: \() 
  - 효율적. 문자와 정수/소수 등의 결합이 자유로움.
```swift
let name = "Taylor"
let age = 26
let message = "Hello, my name is \(name) and I'm \(age) years old."
print(message) 
```

```swift
let number = 11
let missionMessage = "Apollo " + number + " landed on the moon." // error
```

"+" 기호로 문자를 결합할 때는 문자와 숫자를 결합하지 못함. 숫자를 문자로 바꿔줘야 함.
```swift
let missionMessage = "Apollo " + String(number) + " landed on the moon."
```

string interpolation을 사용하면
```swift
let missionMessage = "Apollo \(number) landed on the moon."
```

사칙연산도 가능
```swift
print("5 x 5 is \(5 * 5)") // 5 x 5 is 25
```

왜 Swift에서는 string interpolation을 사용하나? 
사용자로부터 데이터를 받아 처리해야 하기 때문.
```swift
var city = "Cardiff" // 사용자에게 입력받은 값
var message = "Welcome to \(city)!" // 사용자에게 입력받은 값을 처리
```

# 3. [Summary: Simple data](https://www.hackingwithswift.com/quick-start/beginners/summary-simple-data)

* 상수는 let, 변수는 var
* 값의 변화를 의도하지 않는다면 let을 사용해라.

* string은 단문에서 소설 길이까지 가능. 이모지, 전세계언어, count와 윗첨자(uppercased())도 가능.
* string은 시작과 끝에 따옴표로 표시. 줄이 넘어가는 긴 문장은 """ """로 표시.

* integers(정수): 숫자. 양수/음수 가능. isMultiple(of:)
* Double(소수): 100% 정확하지 않으므로 100% 정확해야 하는 곳에는 사용하지 말 것. (예: 돈)
* 사칙연산 "+", "-", "*", "/" => "+="과 같이 간단히 사용 가능.

* Boolean: true/false 값. "!"이나 toggle()로 값 전환 가능.

* String interpolation: 문자, 상수, 변수를 효율적으로 결합할 수 있음. 
