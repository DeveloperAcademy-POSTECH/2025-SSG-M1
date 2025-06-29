## 변수와 상수

### 변수 (Variable)

`var name = "Mosae" name = "Noah" // 변경 가능`

- 값을 변경할 수 있는 데이터
    
- `var` 키워드로 생성
    

### 상수 (Constant)

`let character = "Fine" character = "Echo" // 오류 발생 (값 변경 불가)`

- 한 번 정하면 바꿀 수 없는 데이터
    
- `let` 키워드로 생성
    

---

## 카멜표기법 (camelCase)

- 첫 단어는 소문자, 이후 단어는 대문자로 시작  
    예: `userName`, `totalScore`
    

### 왜 사용하는가?

- 가독성이 좋고, 많은 언어(Java, JavaScript 등)에서 표준처럼 사용됨
    
- 띄어쓰기 대신 일관성 있는 네이밍 가능
    
- 협업 시 코드 스타일 통일
    

---

## 문자열 (String)

### 문자열 선언

`let message = "안녕하세요" print(message)`

- 문자열은 큰 따옴표(`"`)로 감싼다
    
- `print()`를 사용하면 값을 콘솔에 출력할 수 있음
    
- 상수도 출력 가능 (출력 불가는 아님)
    

### 큰 따옴표 포함

`let quote = "Then he tapped a sign saying \"Believe\" and walked away."`

- 큰 따옴표를 넣고 싶으면 `\"` 사용
    

### 줄바꿈 포함 (멀티라인 문자열)

`let movie = """ A day in the life of an Apple engineer """`

---

## 정수 (Int)

### 선언

`let score = 10`

### 가독성을 위한 표기

`let big = 100_000_000`

### 사칙연산

~~~swift
let plus = score + 5 
let minus = score - 2 
let double = score * 2 
let half = score / 2
~~~

### 복합 할당 연산자

~~~swift
var counter = 10 
counter += 5   // 15 
counter *= 2   // 30 
counter -= 10  // 20 
counter /= 2   // 10`
~~~

---

## 배수 확인

`let number = 120 print(number.isMultiple(of: 3)) // true`

- `.isMultiple(of:)` 메서드를 사용해 특정 수의 배수인지 확인
    

---

## 소수 (Double)

### 선언

`let a = 3.1`

- Swift에서는 소수를 기본적으로 `Double` 타입으로 인식
    

> **질문:** Double과 Float의 차이?  
> **답변:** 둘 다 소수를 저장하지만,
> 
> - `Double`: 64비트, 더 정밀
>     
> - `Float`: 32비트, 더 적은 메모리 사용
>     

---

## 타입 혼합 오류

~~~swift
let a = 1     // Int 
let b = 2.0   // Double 
let c = a + b // 오류 발생 (타입이 다름)`
~~~
- `Int`와 `Double`은 다른 타입이므로 함께 연산하려면 형 변환 필요

`let c = Double(a) + b // 가능`

---