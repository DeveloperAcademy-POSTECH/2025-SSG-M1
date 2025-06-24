- **Set는 Array과 유사하지만, Array과 달리 Set에서는 같은 값을 가진 원소를 중복해서 포함할 수 없다.**
- **Set는 순서가 중요하지 않아서 출력할 때 마다 순서가 바뀐다.**
### 선언
- **빈 세트 선언 (Array와 형태가 같기 때문에 명시적으로 Set을 선언해줘여 한다)**
    - var setName = Set<DataType>()
    - var setName: Set<DataType> = []

### 원소 개수
- **setName.count**

### 원소 추가
- **setName.insert(”a”)**

### 빈 배열로 초기화
- **setName = []**


### Set Operation
- **합집합(.union)**
    
    - **setName.union(anoterSet)** setName과 anotherSet의 원소들을 합친 값
    - 
- **차집합(.subtracting)**
    
    - **setName.subtracting(anoterSet)** setName에서 anotherSet의 원소들을 뺀 값
- **대칭차집합(.symmetricDifference)**
    
    - **setName.symmetricDifference(anoterSet)** 합집합에서 교집합을 뺀 값
- **교집합(.intersecrion)**
    
    - **setName.intersecrion(anoterSet)** setName과 anotherSet이 공통으로 가지고 있는 값
- **정렬(.sort, .sorted)**
    
    - **setName.sort()** Set을 오름차순으로 정렬
    - **setName.sorted()** Set을 정렬하지만 사본을 만들어서 정렬
- **조건(true or false)**
    
    let set1: Set = [”A”, “B”]
    
    let set2 : Set = [”A”, “B”, “C”, “D”]
    
    let set3 : Set = [”D”, “E”, “F”]
    
    - **부분집합(.isSubset)** set1.inSubset(of: set2) = true set1이 set2에 포함되어 있는가
    - **모집합(.isSuperset)** set2.isSuperset(of: set1) = true set2가 set1의 모집합인가
    - **교집합의 존재유무(.isDisjoint)** set2.isDisjoint(with: set3) = false set2와 set3 사이에 교집합이 존재하지 않다면 true. →교집합 “D”가 존재하기 때문에 false
