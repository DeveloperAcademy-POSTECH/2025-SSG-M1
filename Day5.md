1. ==**어떻게 조건의 참/거짓을 판단하는가?**==
프로그램들은 자주 선택지를 만든다.
- 만약 시험 성적이 80점을 넘으면 성공 메세지를 띄워라.
- 사용자가 넣은 이름이 알파벳 순으로 친구들의 이름 다음에 와야 한다면 친구들의 이름을 먼저 보여줘라.
- 배열에 숫자를 추가했을 때 아이템 수가 3을 초과한다면, 가장 오래된 것을 삭제하라.
- 사용자에게 이름을 요청했을 때 아무것도 입력하지 않는다면 '익명'이라는 기본 이름을 줘라.

swift는 이런 문제들을 if 구문으로 다룬다. if 문은 조건을 확인해서 조건이 참일 때 실행된다. 그 구조는 아래와 같다.
```swift
if someCondition {
    print("Do something")
}
```

이걸 나눠서 보자.
첫째, 조건은 if와 함께 시작된다. 
둘째, 조건 파트가 참이면, 중괄호 내의 코드: do something 출력을 실행한다.

물론 이것이 코드의 모든 것은 아니다: 나는 { 와 } 에 대해서는 언급하지 않았다.
이것은 braces(중괄호) 라고 불리는데, curly braces 혹은 curly brackets이라고도 불린다.
이 중괄호는 스위프트에서 코드의 블럭을 표시하기 위해 사용된다
이 중괄호 안에 넣고 싶은 만큼의 코드를 마음껏 넣을 수 있다.
```swift
if someCondition {
    print("Do something")
    print("Do something else")
    print("Do a third thing")
}
```

물론 중요한 것은 조건이다. 왜냐면 조건은 어디서 코드를 확인할지 표시하는 곳이기 때문이다.
그럼 점수 예시에서 확인해보자. 80점을 넘었을 때 메세지를 출력해보자.
예시 코드는 다음과 같다.
```swift
let score = 85

if score > 80 {
    print("Great job!")
}
```

이 코드에서, score >80 이 우리의 조건이다. 점수가 80점을 초과할 경우, "Great job!"이 출력될 것이다.
'>' 는 비교 연산자이다. 초과값을 나타낼 때 사용한다. 
'>='는 이상을 의미한다. 

자, 다음 코드는 어떻게 프린트될 것 같은가?
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
 
 speed와 age 조건은 출력되고, percentage 조건은 출력되지 않는다.

이제 우리의 두번째 예시 조건을 시도해보자. 사용자 이름이 친구들의 이름보다 알파벳 순서로 뒤에 온다면, 친구들의 이름을 먼저 보여줘라. 너는 '<', '>=' 그리고 다른 연산자들이 숫자와 어떻게 작용하는지를 이해했다.  연산자는 문자와도 작용할 수 있다.

```swift
let ourName = "Dave Lister"
let friendName = "Arnold Rimmer"

if ourName < friendName {
    print("It's \(ourName) vs \(friendName)")
}

if ourName > friendName {
    print("It's \(friendName) vs \(ourName)")
}
```

따라서, 만약 ourName의 문자가 friendsName보다 알파벳 순으로 먼저 올 경우, 원했던대로 ourName을 먼저 출력하고 그 다음 friendName을 출력할 것이다. 

그럼 세 번째 예시 조건을 보자: 배열에 숫자를 추가했을 때 아이템 수가 3을 초과한다면, 가장 오래된 것을 삭제하라. 

append(), cound, 그리고 remove(at:)을 알고 있으니, 이것들을 함께 사용해 조건을 만들어보자:
```swift
// Make an array of 3 numbers
var numbers = [1, 2, 3]

// Add a 4th
numbers.append(4)

// If we have over 3 items
if numbers.count > 3 {
    // Remove the oldest number
    numbers.remove(at: 0)
}

// Display the result
print(numbers)
```

이제 네 번째 조건을 보자: 만약 사용자가 이름을 요청 받았을 때 아무것도 입력하지 않는다면, '익명'이라는 기본 이름을 주자.

이 문제를 풀기 위해서는 먼저 두 개의 비교 연산자를 이해해야 한다. 첫 번째는 '= ='이고, 같다는 의미이다.

```swift
let country = "Canada"

if country == "Australia" {
    print("G'day!")
}
```

두 번째는 '!='이고, 다르다는 의미이다.

```swift
let name = "Taylor Swift"

if name != "Anonymous" {
    print("Welcome, \(name)")
}
```

예시 코드의 경우 아래와 같이 만들 수 있다.
```swift
// Create the username variable
var username = "taylorswift13"

// If `username` contains an empty string
if username == "" {
    // Make it equal to "Anonymous"
    username = "Anonymous"
}

// Now print a welcome message
print("Welcome, \(username)!")
```

""는 빈값을 의미한다. username을 빈값과 비교하여, 원하는 결과를 얻을 수 있다.

 또 다른 방법으로 확인할 수도 있다.
먼저 우리는 문자의 count를 통해 확인할 수도 있다.

```swift
if username.count == 0 {
    username = "Anonymous"
}
```

어떤 언어에서건 문자를 다른 문자와 비교하는 것은 빠르지 않기 때문에 우리는 정수의 비교로 이를 변환하였다. 문자의 수가 0인가를 확인한 것이다.
이는 대다수의 문자에서 빠르지만, Swift에서는 아니다. Swift는 복잡한 문자를 모두 지원한다. 이모지 같은 것까지 말이다. 
따라서 엄청나게 방대한 문자를 가지고 있다고 했을 때 count == 0을 확인하는 것만으로 시간이 많이 든다. 대신 문자가 하나라도 있으면 우리는 정답이 '아니다'라는 걸 알 수 있다.
결과적으로, isEmpty를 사용하면 빠르게 답을 확인할 수 있다.
```swift
if username.isEmpty == true {
    username = "Anonymous"
}
```

이제 우리는 한 스템 더 나아갈 수 있다. 조건은 참 혹은 거짓이다. 다른 값은 아무것도 나올 수 없다. 따라서 다음과 같이 좀 더 간결하게  코드를 줄일 수 있다.
```swift
if username.isEmpty {
    username = "Anonymous"
}
```

2. ==**어떻게 다수의 조건들을 판단하는가?**==
우리가 if 를 사용할 때 우리는 참/거짓으로 판명될 수 있는 조건을 주어야 한다. 만약 다양한 값을 판단하고 싶다면, 이를 나열할 수 있다.
```swift
let age = 16

if age >= 18 {
    print("You can vote in the next election.")
}

if age < 18 {
    print("Sorry, you're too young to vote.")
}
```

그러나, 이는 효율적인 방식은 아니다. 이 경우 else구문을 이용해 참이 아닌 경우에 대한 실행문을 쓸 수 있다.

```swift
let age = 16

if age >= 18 {
    print("You can vote in the next election.")
} else {
    print("Sorry, you're too young to vote.")
}
```

이렇게 하면 딱 한 번만 나이를 판단하면 된다. 18살이 넘으면 위의 문장을, 낮으면 아래 문장을 출력하면 된다.

심지어 else if 구문을 사용하면 새로운 조건 판단도 가능해진다. else if 와 else를 조합해 쓸 수도 있다. 어쨌거나 else는 딱 한 번만 사용할 수 있다.

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

또한 다음과 같이 한 개 이상의 조건을 판단하도록 할 수도 있다.
```swift
let temp = 25

if temp > 20 {
    if temp < 30 {
        print("It's a nice day.")
    }
}
```
더 짧은 대체 형식도 있다. &&를 사용하면 가능하다.
```swift
if temp > 20 && temp < 30 {
    print("It's a nice day.")
}
```

&&는 'and' 조건이다. ||는 'or' 조건이다. &&는 두 조건 모두 참일 때, ||는 둘 중 하나 이상이 참일 때 실행된다.
```swift
let userAge = 14
let hasParentalConsent = true

if userAge >= 18 || hasParentalConsent == true {
    print("You can buy the game")
}
```
참고로 위 조건에서 '== true' 부분은 생략될 수 있다.

3. ==**어떻게 switch 구문을 사용하여 다수의 조건을 판단하는가?**==
if와 else if 를 반복적으로 사용해 조건들을 계속 확인할 수 있지만, 읽기가 좀 어렵다. 이때 switch 구문을 활용할 수 있다.

```swift
switch forecast {
case .sun:
    print("It should be a nice day.")
case .rain:
    print("Pack an umbrella.")
case .wind:
    print("Wear something warm")
case .snow:
    print("School is cancelled.")
case .unknown:
    print("Our forecast generator is broken!")
}
```

이때 switch 구문은 답으로 올 수 있는 모든 값을 커버할 수 있어야 한다. 따라서 default를 사용한다.

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

그리고 자주 쓰이는 것은 아니지만, fallthrough을 사용하면 연속되는 케이스들을 계속 수행하도록 할 수 있다.
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

4. ==**어떻게 삼항 연산자를 이용해 빠른 테스트를 할 수 있을까?**==
이항 연산자: 2+5 처럼 항이 두 개인 것.
삼항 연산자: 3개의 입력값으로 작동하는 것.

```swift
let age = 18
let canVote = age >= 18 ? "Yes" : "No"
```

이 코드가 실행되면, canVote값은 'Yes'가 될 것이다. 왜냐면 age가 18이기 때문이다.
값이 참이면 'Yes'가, 거짓이면 'No'가 주어진다. 이런 점에서 if 그리고 else문과 같다.

다른 예문을 보자. 

```swift
let names = ["Jayne", "Kaylee", "Mal"]   
let crewCount = names.isEmpty ? "No one" : "\(names.count) people"
print(crewCount)
```

name 배열이 비어있으면 "No one" 값을, 그렇지 않으면 names에 속한 값의 수 + people을 crewCount에 반환한다.

'= ='연산자를 사용하면 조금 읽기 어려워진다.
```swift
enum Theme {
    case light, dark
}

let theme = Theme.dark

let background = theme == .dark ? "black" : "white"
print(background)
```
간단하게 보자. theme == .dark인가?
맞다면, black을, 틀리다면, white를 반환한다.