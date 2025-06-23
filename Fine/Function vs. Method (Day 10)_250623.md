# [What’s the difference between a function and a method?](https://www.hackingwithswift.com/quick-start/understanding-swift/whats-the-difference-between-a-function-and-a-method)

* 공통점: 함수, 메서드 모두 기능의 일부에 이름을 지정하고 반복적으로 실행.
* 차이점
	* 메서드: 구조체, 열거형, 클래스와 같은 타입에 속함.
	* 함수: 타입에 속하지 않음.
* 메서드의 장점
	* 해당 유형 내의 다른 속성과 메서드를 참조할 수 있음. 
	* _네임스페이스 오염을_ 방지
		* 함수를 그냥 만들면 이름이 코드 전체에서 예약되어 네임스페이스 오염이 생김. 100개의 함수를 만들면 100개의 이름이 생김. 예) wakeUp() => 코드 전체에서 wakeUp이라는 함수 이름이 예약됨.
			* 메서드로 만들면, 객체 안에서만 의미가 있으니, 코드 전체에 이름이 퍼지지 않고 오염이 줄어듦. 예) someUser.wakeUp() - wakeUp이 코드 전체가 아니라 someUser 안에서만 의미를 가짐. someUser.wakeUp(), otherUser.wakeUp() 과 같은 식으로 구분 가능.
		* 그래서 많은 기능을 메서드로 만들면, 이름 충돌이나 헷갈림을 줄일 수 있음.