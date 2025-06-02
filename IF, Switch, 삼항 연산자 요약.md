[If 문의 기본 구조]

```swift
if someCondition {
    print("Do something")
}
```

[비교 연산자]
초과: '>', 이상: '>=', 미만 '<', 이하 '<='

```swift
let speed = 88
let percentage = 85
let age = 18

if speed >= 88 {
    print("Where we're going we don't need roads.")
}

if percentage < 85 {
    print("Sorry, you failed the test.")
}

if age >= 18 {
    print("You're eligible to vote")
}
```
- 문자도 대소비교가 가능하다: 알파벳의 순서

같다 '= =' 다르다 '!='

```swift
let country = "Canada"

if country == "Australia" {
    print("G'day!")
}

```swift
let name = "Taylor Swift"

if name != "Anonymous" {
    print("Welcome, \(name)")
}
```
- 조건문에서 '= = true'는 생략될 수 있다.

[여러 조건 비교]
&&는 'and' 조건이다. ||는 'or' 조건이다. &&는 두 조건 모두 참일 때, ||는 둘 중 하나 이상이 참일 때 실행된다.
```swift
let userAge = 14
let hasParentalConsent = true

if userAge >= 18 || hasParentalConsent == true {
    print("You can buy the game")
}
```

if, else if, else를 활용한다. Else는 딱 한 번만 사용 가능하다.
else if는 원하는만큼 사용 가능하다.

```swift
let a = false
let b = true

if a {
    print("Code to run if a is true")
} else if b {
    print("Code to run if a is false but b is true")
} else {
    print("Code to run if both a and b are false")
}
```

[Switch 구문]
switch 구문은 답으로 올 수 있는 모든 값을 커버할 수 있어야 한다. 기본값을 default로 적용하여 사용한다.

```swift
let place = "Metropolis"

switch place {
case "Gotham":
    print("You're Batman!")
case "Mega-City One":
    print("You're Judge Dredd!")
case "Wakanda":
    print("You're Black Panther!")
default:
    print("Who are you?")
}
```

자주 쓰이는 것은 아니지만, fallthrough을 사용하면 연속되는 케이스들을 계속 수행하도록 할 수 있다.
```swift
let day = 5
print("My true love gave to me…")

switch day {
case 5:
    print("5 golden rings")
    fallthrough
case 4:
    print("4 calling birds")
    fallthrough
case 3:
    print("3 French hens")
    fallthrough
case 2:
    print("2 turtle doves")
    fallthrough
default:
    print("A partridge in a pear tree")
}
```

[삼항 연산자]
삼항 연산자: 3개의 입력값으로 작동하는 것.
```swift
let age = 18
let canVote = age >= 18 ? "Yes" : "No"
```
