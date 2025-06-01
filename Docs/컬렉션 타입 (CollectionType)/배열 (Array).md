### **선언
##### 빈배열 선언
	- var arrayName : [DateType] = []
	- var arrayName = Array<DateType>()
	- var arrayName : Array<DateType> = []
	- var arrayName = [DateType]()

##### **특정값을 포함한 배열 선언
	- var shoppingList: [String] = [”Eggs”, “Milk”]

##### **특정 값이 반복되는 배열 선언
	- var threeDouble = Array(repeating: 0.0, count: 3)
		- [0.0, 0.0, 0.0]

### **배열 편집
##### 원소의 개수를 새는 메서드 (.count)
	arrayName.count

---
##### **원소를 추가하는 메서드 (.append, .insert)
- **arrayName배열 안에 22라는 원소를 추가한다.
	- `arrayName.append(22)`

- **arrayName에 원소 33, 44를 추가한다. (원소를 포함한 배열을 추가)
	- `arrayName += [33, 44]`

- **0번 인덱스에 22라는 원소를 추가한다. 
	- ` arrayName.insert(22, at: 0)
 >(기존에 해당 인덱스에 있는 원소는 제거되지 않고 뒤로 밀린다.)

---

##### **원소를 제거하는 메서드 (.remove)
- **arrayName배열 안에 22라는 제거한다.
	- `arrayName.remove(22)
- **arrayName배열 안에 0번 인덱스에 해당하는 원소를 제거한다.
	- `arrayName.remove(at: 0)

---
##### **빈 배열인지 확인하는메서드 (.isEmpty)
- **배열이 비어있으면 true 비어있지 않으면 false
	- arrayName.isEmpty

---
##### **특정원소가 들어있는지 확인하는 메서드 (.contains)
- **배열안에 특정원소가 있다면 true 없다면 false
	- `arrayName.contains("????")

---
##### **원소를 정렬하는 메서드 (.sort, .reverse)
###### .sort
- **배열을 오름차순으로 정렬한다.
	- `arrayName.sort()
- **배열을 내림차순으로 정렬한다.
	- `arrayName.sort(by: >)
###### **.sorted
- **.sort와 같이 오름 내림차순으로 정렬한다. 차이점은 새로운 정렬된 배열을 새롭게 리턴한다.
	- `arrayName.sorted()
###### **.reverse
- **배열을 뒤집는다.
	- `arrayName.reverse()
- ![[스크린샷 2025-06-01 오후 4.41.23.png]] 뒤집는 방식은 양쪽 인덱스의 원소들을 바꾸는 방식
	  때문에 시간 복잡도가 O(n)이다.
###### **.reversed
- **.reverse와 다르게 단순히 배열을 반대로 읽는 것이다.
	- `arrayName.reversed()
- ![[스크린샷 2025-06-01 오후 4.44.19.png]]

---


##### **빈 배열로 초기화하는 메서드
	arrayName = []
	
---
##### 인덱스로 배열에 접근하는 메서드
- 0번 인덱스의 원소에 접근한다.
	- `arrayName[0] = 22`

---
##### 배열안의 원소를 호출하는 메서드
- **arrayName배열 안의 원소들을 인덱스 순서대로 호출한다.
	- `for item in arrayName{}`
- **.enumerated는 원소의 값과 함께 인덱스도 출력하게 해준다. (ex. index: 0: 22)
	- `for (index, value) in arrayName.enumerated() {}`

---