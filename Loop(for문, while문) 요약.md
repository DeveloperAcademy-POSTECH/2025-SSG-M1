
[for 문의 기본 구조]
배열, 세트, 딕셔너리 등을 활용한다.

```swift
let platforms = ["iOS", "macOS", "tvOS", "watchOS"]

for os in platforms {
    print("Swift works great on \(os).")
}
```

- 괄호 안의 값을 '반복문(loop body)'이라고 부른다.
- 반복문의 한 사이클을 '반복(loop iteration)'이라고 부른다.
- 우리는 os를 반복 변수(loop variable)이라고 부른다. 이것은 반복문 안에서만 존재하며, 다음 반복(loop iteration) 시에는 새로운 값으로 바뀐다.

 범위(Range)를 활용할 수도 있다.
```swift
for i in 1...12 {
    print("5 x \(i) is \(5 * i)")
}
```

[중첩반복문]

```swift
for i in 1...12 {
    print("The \(i) times table:")

    for j in 1...12 {
        print("  \(j) x \(i) is \(j * i)")
    }

    print()
}
```
 - print()를 통해 줄을 구분할 수 있다. 코드가 읽기 쉬워진다.

[range]
```swift
for i in 1...5 {
    print("Counting from 1 through 5: \(i)")
}

print()

for i in 1..<5 {
    print("Counting 1 up to 5: \(i)")
}
```
- ..<를 사용하면 마지막 값을 포함하지 않는다.

i, j 같은 반복 변수를 사용하고 싶지 않다면, underscore로 이것을 대체할 수 있다.
```swift
var lyric = "Haters gonna"

for _ in 1...5 {
    lyric += " hate"
}

print(lyric)
```

[While문의 기본구조]

```swift
var countdown = 10

while countdown > 0 {
    print("\(countdown)…")
    countdown -= 1
}

print("Blast off!")
```

[.random 메소드]

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
- Int, doouble에서 사용하며 범위 내의 랜덤값을 반환한다.

[Continue]
continue를 사용하면, 지금의 반복을 그만두고 반복문의 다음 변수값으로 넘어간다. 

```swift
let filenames = ["me.jpg", "work.txt", "sophie.jpg", "logo.psd"]

for filename in filenames {
    if filename.hasSuffix(".jpg") == false {
        continue
    }

    print("Found picture: \(filename)")
}
```

[Break]
남은 반복을 모두 중단시킨다.

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
