# # Step3. 함수 역할 분리

- 개발한 것(배운 것)

	#####1. 객체를 별도 파일에 생성하면서 main.swift 에서는 분리한 객체들 인스턴스끼리 조합하기

	: step3에서는 하나의 파일에 메소드를 쭉 나열하듯 쓰던 코드를 역할에 따라 객체 별로 분리하여 작성하는 연습을 했다. 그러다보니 기능에 대한 소속(?)을 정하는 데 어려움을 겪었다.(ex, makeRandomValue())  
	또한 private에 대한 필요성을 잘 못느껴서 몽땅 public으로 뒀었는데 객체 내에서만 사용하는 메소드나 프로퍼티에서는 private으로 쓰는 게 좋다는 피드백을 받았다.  
	이번 step에서 JK의 많은 피드백만큼 배운 것도 많았다:)

- 피드백

	https://github.com/dely2p/swift-laddergame/issues/3  
	https://github.com/dely2p/swift-laddergame/issues/4  
	https://github.com/dely2p/swift-laddergame/issues/5  
	https://github.com/dely2p/swift-laddergame/issues/6  
	https://github.com/dely2p/swift-laddergame/issues/7  
	https://github.com/dely2p/swift-laddergame/issues/8  
	https://github.com/dely2p/swift-laddergame/issues/9  
	https://github.com/dely2p/swift-laddergame/issues/10  
	https://github.com/dely2p/swift-laddergame/issues/11  
	https://github.com/dely2p/swift-laddergame/issues/12  
	https://github.com/dely2p/swift-laddergame/issues/13  
	https://github.com/dely2p/swift-laddergame/issues/14  
	https://github.com/dely2p/swift-laddergame/issues/15  
	https://github.com/dely2p/swift-laddergame/issues/16  
	https://github.com/dely2p/swift-laddergame/issues/17    
	

- 알게 된 것

	1. 접근제어 지정하기  
	: private에 익숙치 않았다. 그냥 데이터는 바로 접근해서 쓰는 것에 익숙해서;; 나만 쓰는 프로그램이 아닌 다른 사람들도 쓰는 프로그램을 만들기 위해서는 접근 제어를 위해 직접 접근하기보단 메소드를 통해서 가져오도록 해야 한다.

	2. 입력 값에 대한 예외처리 하기  
	: `!`에서 벗어나기 프로젝트가 시작되었다. 강제 옵셔널은 프로그램을 죽게 만들뿐만 아니라 

		```swift
		 let temp = readLine()!
		 heightForLadder = Int(temp)!
		```
		
		 ```swift
		 if let temp = readLine() {
		 		guard let heightForLadder = Int(temp) else {
		 			return 
		 		}
		 }
		 ```
	 

	3. 메소드 역할에 따라 어떤 객체에 둘 지 정하기
		- makeRandomValue() 메소드는 LadderGame에서 사다리의 bar를 놓을지 안놓을지 정할 때 사용 할 랜덤 숫자를 만들게 된다.  
		그래서 처음에는 OutputView 객체에 두었는데 피드백을 받고 생각해보니 OutputView는 출력관련 기능만 두고 LadderGame 객체에서 사용하고 해당 데이터만 넘기는 것이 효율적이었다.
		- 원래 유저의 이름을 갖는 LadderPlayer객체를 main에서 생성하도록 만들었다. InputView에서는 사용자로부터 이름데이터를 입력받는데에 집중하고 main에서 LadderPlayer객체를 생성하고 append해서 LadderGame에게 넘겨줘야한다고 생각했기 때문이었다. 하지만 main은 객체간의 controller일 뿐.. 기능 상 가장 가까운 InputView에 메소드로 만들어서 두는 게 더 좋았다.

	4. 주석 지우기
		- 학부시절 날아간 코드 때문에 프로그램을 새로 다시짰던 안좋은 기억이 있다. 그래서 왠만하면 코드를 안지우는 습관을 갖게 되었다. 몽땅 주석처리.. 언제쓸지 다시 되살릴지 모르니.. 그런데 깃을 쓰면서는 사실 필요없는 습관이었다. 커밋만 잘 해뒀으면 다 남아있으니ㅎㅎ 

	5. private (set)
		- private은 봤지만 private (set)은 처음 봤다. 프로퍼티의 set은 막지만 get은 허용하는 유용한 설정 방식이었다. 코드를 매우 깔끔하게 보여지도록 만든다.

	6. `반복되는 메소드 호출`보다 `데이터 구조`
		- 사다리를 그릴 때 매번 랜덤값을 호출하도록 구현했다. 랜덤값이 필요하니까 호출해야지 마인드였던 것 같다. 이렇게 되면 만약 커다란 프로그램 구현 시에는 프로그램이 매우매우매우매우 느려진다. 고로 이차원 배열과 같은 데이터구조를 갖도록 만드는 것이 더 좋다.

	7. 고차함수 map
		- ```
		let nameOfSeparate = ladderGameInfo.nameOfPlayer.split(separator: ",").map({String($0)}).map({LadderPlayer(name: $0)})
		```
		이 코드는 입력받은 String을 콤마를 기준으로 나누고 하나씩 가져와서 하나씩 LadderPlayer에 넣는 기능을 한 줄로 표현한 map의 어마어마어마함을 보여주는 코드다.