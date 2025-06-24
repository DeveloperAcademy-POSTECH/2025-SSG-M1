### 선언

- **빈 Dictionary 선언** Int를 Key값으로 받고 String를 Value로 받는 Dictionary 선언하기
    - **var dictionaryName: [Int: String] = [:]**
    - **var dictionartName: Dictionart<Int, String> = [:]**
    - **var dictionartName = Dictionary<Int, String>()**

### 원소 개수
- **dictionaryName.count**

### 원소 추가

- **dictionaryName[Key] = Value** dictionaryName = [Key: Value]
    - 해당 Key가 없다면, 추가 (insert)
    - 해당 Key가 있다면, Value 덮어쓰기 (update)

- **dictionaryName.updateValue(Value, forKey: Key)**
    - 해당 Key가 없다면, 추가하고 nil 리턴 (insert)
    - 해당 Key가 있다면, Value 덮어쓰고 덮어쓰기 전 값 리턴 (update)

### Dictionary 초기화

- **dictionaryName = [:]**