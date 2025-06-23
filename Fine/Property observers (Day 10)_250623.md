# [How to take action when a property changes](https://www.hackingwithswift.com/quick-start/beginners/how-to-take-action-when-a-property-changes)

* 속성 관찰자(Property observer): 속성이 변경될 때 실행되는 특수 코드. 
	* 이 관찰자는 두 가지 형태를 가짐. 
		* `didSet`: 속성이 방금 변경되었을 때 실행되는 관찰자 
		* `willSet`: 속성이 변경되기 _전에_ 실행되는 관찰자

```swift
struct Game {
    var score = 0
}

var game = Game()
game.score += 10
print("Score is now \(game.score)")
game.score -= 3
print("Score is now \(game.score)")
game.score += 1
```

Game 구조체에서 점수 수정. 점수가 변경될 때마다 `print()`변경 사항을 추적할 수 있도록 줄을 추가함. 그런데 마지막에 점수가 변경되었는데, 점수가 출력되지 _않음, 실수.

속성 관찰자를 사용하면 속성이 변경될 때마다(어디에서 변경되든) 항상 일부 코드를 실행하게 함.
```swift
struct Game {
    var score = 0 {
        didSet {
            print("Score is now \(score)")
        }
    }
}

var game = Game()
game.score += 10
game.score -= 3
game.score += 1
```
