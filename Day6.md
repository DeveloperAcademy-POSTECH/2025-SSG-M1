==**1. 어떻게 반복적인 작업을 위해 loop를 활용할까? ==**

컴퓨터는 반복적인 작업을 하기에 아주 뛰어나며, 스위프트는 코드를 반복하거나 배열, 딕셔너리, 세트의 모든 값을 손쉽게 실행한다.
간단히 시작해보자. 우리가 문자의 배열을 가지고 있다고 할 때, 우리는 각 문자열을 이렇게 출력할 수 있다:

```swift
let platforms = ["iOS", "macOS", "tvOS", "watchOS"]

for os in platforms {
    print("Swift works great on \(os).")
}
```

여기서는 platforms에 속하는 모든 값을 os에 반복한다. 우리는 os를 다른 곳에 선언하지 않았고, 단지 반복문의 형태로 괄호 안에서만 사용하기 위해 형성했을 뿐이다.

괄호 안에는 배열의 모든 값마다 실행하고 싶은 코드가 있고, 따라서 위의 코드는 네 줄을 출력할 것이다. 배열의 값마다 한 줄씩. iOS, macOS, tvOS, watchOS 각 값마다 한 번씩 print()를 호출할 것이다.

이해하기 쉽게, 여기에 이름을 붙였다.
- 괄호 안의 값을 '반복문(loop body)'이라고 부른다.
- 반복문의 한 사이클을 '반복(loop iteration)'이라고 부른다.
- 우리는 os를 반복 변수(loop variable)이라고 부른다. 이것은 반복문 안에서만 존재하며, 다음 반복(loop iteration) 시에는 새로운 값으로 바뀐다.

os는 특별한 이름이 아니다. 이렇게 적을 수도 있다.

```swift
for name in platforms {
    print("Swift works great on \(name).")
}
```

이렇게 적어도 코드는 동일하게 작동한다.

사실 Xcode는 정말 똑똑하다.  만약 당신이 for plat을 적으면, 즉시 platforms라는 배열이 있다는 사실을 알아차릴 것이고, for platfrom in platforms라고 자동완성을 제공할 것이다. platforms가 복수형이라는 사실을 알아채고 반복 변수로 단수형을 제시할 것이다. 

배열을 반복하는 대신 정해진 범위의 숫자를 반복할 수도 있다. 예를 들어 1에서 12까지 5번의 테이블을 출력할 수도 있다.

```swift
for i in 1...12 {
    print("5 x \(i) is \(5 * i)")
}
```

몇 가지의 새로운 사실을 알 수 있다.

- 반복 변수로 i를 사용했다. 두 번째 숫자를 셀 때는 보통 j를, 세 번째를 셀 때는 k를 사용한다. 네 번째를 셀 때는 좀 다른 이름을 택해야 할 것이다.
- 1...12 부분은 range(범위)라고 불린다. 그리고 이것은 1과 12를 포함한 1부터 12까지의 정수 모두를 의미한다. ranges는 스위프트의 고유한 데이터 타입이다.

따라서, 위의 코드는 i가 처음에는 1이 되고, 그 뒤에는 2가 되고, 그리고 3, 등등, 12까지 된 다음 반복문을 종료할 것이다.

반복문 안에 반복문을 중첩할 수도 있다. 이것을 nested loops(중첩 반복)이라고 부른다.

```swift
for i in 1...12 {
    print("The \(i) times table:")

    for j in 1...12 {
        print("  \(j) x \(i) is \(j * i)")
    }

    print()
}
```

이것도 새로운 사실을 몇 가지 보여준다.

- 중첩반복문이다. 1부터 12까지 셀 것이고, 각 숫자의 안에서 다시 1부터 12까지 셀 것이다.
- print()를 사용하면서 아무것도 안에 없기 때문에, 그저 새로운 줄로 시작할 것이다. 이것은 결과를 나누어 보기에 좋다. (코드가 깔끔해진다.)

따라서 우리는 x...y 를 보면 x의 값이 무엇이든간에 거기서 시작해서, y의 값까지 반복한다는 사실을 알 수 있다. (x와 y값 포함)

스위프트는 비슷하지만 다른 타입의 range도 제공한다. 마지막 값을 배제하는 범위이다. ..< 으로 표현되며 코드에서는 이렇게 쓰인다.

```swift
for i in 1...5 {
    print("Counting from 1 through 5: \(i)")
}

print()

for i in 1..<5 {
    print("Counting 1 up to 5: \(i)")
}
```

반복문을 사용할 때 i, j 같은 반복 변수를 사용하고 싶지 않다면, underscore로 이것을 대체할 수 있다.

```swift
var lyric = "Haters gonna"

for _ in 1...5 {
    lyric += " hate"
}

print(lyric)
```

==**2. 어떻게 반복적인 작업을 위해 while문을 사용할까? ==**

두번째 반복문은 while이다. 조건을 지니고 있으며 조건이 거짓이 될 때까지 반복한다. while문은 for문만큼 자주 쓰이지는 않는다. 따라서 이해는 하되 너무 깊게 파고들 필요는 없다.

기초적인 while문은 이렇다.

```swift
var countdown = 10

while countdown > 0 {
    print("\(countdown)…")
    countdown -= 1
}

print("Blast off!")
```

정수 10에서 시작하며 while문을 반복한다. 반복문 내에서 countdown의 값을 1씩 감소시켜 0과 같거나 그보다 작은 값이 되면 반복문이 종료되고 마지막 메세지가 출력된다.

while문은 몇 번이나 출력해야 할지 정확하지 않을 때 아주 유용하다. 이를 증명하기 위해 int와 double에서 사용 가능한 random(in:)이라는 메소드를 소개하겠다. 범위 내의 랜덤한 값을 반환하는 메소드이다.

예를 들어 1과 1000 사이에서 랜덤한 정수를 반환하는 예시이다.

```swift
let id = Int.random(in: 1...1000)
```

그리고 이건 0과 1사이의 소수를 랜덤 반환하는 예시이다.

```swift
let amount = Double.random(in: 0...1)
```

우리는 20면 주사위를 반복해서 던지는 상황을 가정하기 위해 이 메소드를 while 문과 함께 사용할 수 있다.

```swift
// create an integer to store our roll
var roll = 0

// carry on looping until we reach 20
while roll != 20 {
    // roll a new dice and print what it was
    roll = Int.random(in: 1...20)
    print("I rolled a \(roll)")
}

// if we're here it means the loop ended – we got a 20!    
print("Critical hit!")
```

즉, for문을 훨씬 자주 사용하지만, 조건을 통해 반복문을 사용할 때는 while문이 유용하다.

==**3. 어떻게 반복문에서 값을 skip할 수 있을까? (with break & continue) ==**

스위프트에서는 반복문에서 하나 혹은 여러 값을 스킵할 수 있다. continue는 지금의 반복을 스킵할 수 있고, break는 남은 모든 반복을 건너 뛸 수 있다. 

continue부터 하나씩 살펴보자. 반복문에서 continue를 사용하면, 지금의 반복을 그만두고 반복문의 다음 변수값으로 넘어간다. 

```swift
let filenames = ["me.jpg", "work.txt", "sophie.jpg", "logo.psd"]

for filename in filenames {
    if filename.hasSuffix(".jpg") == false {
        continue
    }

    print("Found picture: \(filename)")
}
```

접미사 .jpg를 가지고 있지 않은 Filename에 대해서는 continue를 통해 반복문을 스킵한다.

break에 대해서는, 남은 반복을 모두 중단시킨다.

```swift
let number1 = 4
let number2 = 14
var multiples = [Int]()

for i in 1...100_000 {
    if i.isMultiple(of: number1) && i.isMultiple(of: number2) {
        multiples.append(i)

        if multiples.count == 10 {
            break
        }
    }
}

print(multiples)
```

두 상수를 만든다. 두 값의 공배수를 저장할 정수 배열을 만든다. i값에 대해 1부터 10000까지 반복한다. i가 두 값의 공배수이면 append를 사용해 배열에 추가한다. 만약 10개의 변수가 저장되면, 반복문을 break한다. 배열을 출력한다.


==**4. 조건문과 반복문 요약==**

- 조건문이 참인지 확인하기 위해 if문을 사용한다. 어떤 조건이든 넣을 수 있으나, 참/거짓으로 판명되어야 한다.
- else 블럭을 사용하거나 else if를 사용해 다른 조건들을 살피도록 할 수 있다. 순서대로 실행될 것이다.
- ||(or)와 &&(and)를 사용해 여러 조건을 조합할 수 있다. 
- 만약 여러 조건을 반복적으로 체크한다면, Swich구문을 사용하라. 반드시 모든 조건을 포괄해야 하므로, default 케이스를 사용하라.
- switch 문에 fallthrough을 사용하면, 연쇄되는 조건을 실행하라는 의미이다. 자주 사용되진 않는다.
- 3항 연산자는 무엇인지(조건), 참값, 거짓값을 확인할 수 있게 한다. 처음엔 좀 읽기 어렵지만 자주 사용된다.
- for 반복문은 배열, 세트, 딕셔너리, 그리고 범위(range)를 반복하게 한단. 반복 변수를 주거나 underscore를 사용할 수 있다.
- while문은 조건에 따른 반복문을 사용하는데 유용하다.
- continue와 break를 이용해 반복문을 스킵할 수 있다.

==**5. Check Point 3 ==**

조건문과 반복문을 사용할 수 있게 됐으니 fizz buzz라고 불리는 문제를 풀어보자. 목표는 1부터 100까지 반복하는 것이고,

1. 3의 배수이면 "Fizz"를 출력한다.
2. 5의 배수이면 "Buzz"를 출력한다.
3. 3과 5의 공배수이면 "FizzBuzz"를 출력한다.
4. 다른 경우, 그냥 숫자를 출력한다.

어려우면 힌트가 있다.

1. 배수인지 확인하기 위해서는 .isMultiple(of: )를 사용한다.
2. 3과 5를 먼저 체크해라. 이게 가장 좁은 범위의 조건이다. 그 다음 3을, 그 다음 5를, 그리고 else 블럭을 사용해서 나머지 숫자를 다뤄라.
3. && 를 사용해 3과 5의 공배수를 찾는 조건을 만들 수 있다. 아니면 그냥 if문을 중첩해도 된다.
4. 1부터 100까지의 범위를 반복하려면 ..< 보다는 ...를 사용해라.