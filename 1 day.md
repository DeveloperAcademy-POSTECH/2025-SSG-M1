## 변수와 상수

#### 변수
~~~swift
var name = "Mosae" 
name = "Noah" // 변경 가능
~~~

**GQ. 변수는 뭐지?**  
= 값을 변경할 수 있는 데이터. 
`var` 키워드를 사용해 생성.

#### 상수

~~~swift
let character = "Fine" character = "Echo" // 오류 발생 (값 변경 불가)
~~~

**GQ. 상수는 뭐지?**  
= 한 번 정하면 바꿀 수 없는 데이터. 
`let` 키워드를 사용해 생성.

---

## 카멜표기법 (camelCase)

첫 단어는 소문자, 이후 단어는 대문자로 시작  
예: `userName`, `totalScore`

**GQ. 왜 카멜표기법을 사용하지?**  
- 가독성 향상
- 프로그래밍의 표준 명명 규칙(Java, JavaScript 등)이기에 일관성 유지
- 띄어쓰기 불가 환경에서의 대안
- 일관된 협업을 위함.

---

## 문자열

문자열은 큰따옴표 `" "` 안에 작성함.

~~~swift
let message = "안녕하세요" 
print(message)
~~~

print()는 변수의 값을 콘솔에 출력함.

**GQ. 그럼 상수는 출력이 안되나?**
상수도 출력 가능함. 값만 못 바꿈.

**GQ. 문자열 안에 큰따옴표를 넣으려면?**
~~~swift
let quote = "He said, \"Hello\""
~~~
= 역슬래시, 큰따옴표(\")를 넣으면 됨.

**GQ. 문자열을 줄바꿈하고 싶다면?**
~~~swift
let text = """ Line 1 Line 2 """
~~~
= 세 개의 큰 따옴표(""")를 넣으면 됨.

---

## 세미콜론

Swift는 세미콜론(;)이 필요 없음  
= 한 줄의 끝을 자동으로 인식함.

**GQ. 세미콜론은 왜 쓰는거지?**
= 세미콜론은 한 줄의 명령어가 끝났다는 것을 알려주는 기호.
swift는 자동으로 줄 끝을 인식하지만, 다른 언어들은 그렇지 않기에 직접 써야함.

---

## 정수 (Int)

정수는 소수 없는 '온전한 수' (3, 10 등)
Swift에서는 Int라는 자료형을 씀.
~~~swift
let score = 10 // 상수(let) 정수(10) 선언
~~~

**GQ. 긴 숫자를 읽기 쉽게 쓰는 방법은?**
= 밑줄(_)로 구분하여 쉽게 쓸 수 있음.
~~~swift
let big = 100_000_000 // 보기 쉽다!
~~~

**GQ. 사칙연산을 하는 방법은?**
~~~swift
let plus = score + 5 
let minus = score - 2 
let mult = score * 2 
let div = score / 2
~~~

#### 복합 할당 연산자
**GQ. 복합 할당 연산자가 뭐지?**
= 값을 더하거나 뺄 때 코드를 짧게 쓰는 법을 '복합 할당 연산자'라고 함.

'counter = counter + 5' 
대신 
'counter += 5' 
(코드가 짧고 간단해짐)

~~~swift
var counter = 10 
counter += 5 
counter *= 2 
counter -= 10 
counter /= 2
~~~

---

## 배수 확인

**GQ. 어떻게 특정 수의 배수를 확인할 수 있을까?**
~~~swift
let number = 120 
print(number.isMultiple(of: 3)) // true
~~~
**해석:**
let number = 120
-> 숫자 120을 number라는 이름으로 저장함.

number.isMultiple(of: 3)
-> “이 숫자(number)가 3의 배수인지?“를 물어보는 코드.

print(...)
-> 결과를 화면에 출력.

**결과:**
120은 3 × 40 = 120이니까 **3의 배수**가 맞지?
그래서 true가 출력돼. (참이라는 뜻)

---

## 소수 (Double)

~~~swift
let a = 3.1 // Double로 자동 인식
~~~
- Double: 64비트, 정밀도 높음
- Float: 32비트, 가볍고 빠름

---

**GQ. 서로 다른 타입의 코드를 연산할 수 있을까?**
= 타입간의 혼합은 불가. 

~~~swift
let a = 1     // Int 
let b = 2.2   // Double 
let c = a + b // 에러
~~~

---

