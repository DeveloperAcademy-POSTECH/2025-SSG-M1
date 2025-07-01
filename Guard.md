1. 기본 문법

```swift
guard 조건 else {
  // 조건이 false일 때 실행되는 코드 (예: 함수 종료, return, break 등)
    return
}
// 조건이 true일 때 아래 코드 계속 실행됨
```
  
예시)
```swift
guard let name = name, !name.isEmpty else {
        print("이름이 없습니다.")
        return
    }
    
guard let name = name, !name.isEmpty else {
    // name이 nil이거나, 빈 문자열이면 여기로
    return

}
    ```

2. guard VS guard let

|**구문**|**의미**|**설명**|
|---|---|---|
|guard 조건 else { ... }|일반 조건 확인|조건이 **false면 탈출**, true면 계속 실행|
|guard let x = optional else { ... }|옵셔널 바인딩|optional이 **nil이면 탈출**, nil이 아니면 x에 안전하게 바인딩|

3. 왜 사용할까?
 guard는 중첩을 줄이고 early exit
 
4. 사용 규칙
- else 블록 안에서 반드시 **탈출(return, break, continue, throw)** 해야 함
- guard let을 쓰면 옵셔널 바인딩 결과를 이후 코드에서 **비옵셔널로 안전하게 사용** 가능 
- 조건이 실패하면 **즉시 함수 또는 블록에서 빠져나간다**

\*옵셔널 바인딩
옵셔널에 값이 있을 때만 그 값을 꺼내서 사용할 수 있게 해주는 문법

```swift
var name: String? = "Jin"

if let unwrappedName = name {
    print("안녕하세요, \(unwrappedName)님!")  // ✅ 여기서 unwrappedName은 String
} else {
    print("이름이 없습니다.")
}
```