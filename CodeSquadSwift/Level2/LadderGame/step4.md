# # Step4. 함수 역할 분리

- 개발한 것(배운 것)

	#####1. 콘솔 입/출력를 제외한 나머지 모든 소스 코드에 있는 모든 메서드에 대한 단위 테스트 로직을 구현한다.

	: step4에서는 어마무시한 테스트코드 구현을 배웠다. 테스트코드를 작성하면서 나는 내 코드에 대한 원망을 하게되었다. 기능 별로 쪼개서 짰어야 하는데.. 데이터를 넘겨주도록 짜야하는데.. 엉망이었다. 그래서 테스트를 할 수 없었다.ㅠㅠ 그래서 InputView부터 엄청 뜯어고쳤다;;;;; 엉엉ㅠㅠ
	
	
- 피드백

	https://github.com/dely2p/swift-laddergame/issues/18  
	https://github.com/dely2p/swift-laddergame/issues/19  
	https://github.com/dely2p/swift-laddergame/issues/20  
	https://github.com/dely2p/swift-laddergame/issues/21  
	https://github.com/dely2p/swift-laddergame/issues/22  
	https://github.com/dely2p/swift-laddergame/issues/23  

  
- 알게 된 것

	1. Data Object의 필요성 (LadderGameInfo)  
		: 이전에는 사실 Data Object가 왜 필요하나.. 그냥 다이렉트로 넘기면되지.. 귀찮.. 이런 생각이 들었는데 테스트 코드 작성을 하다보니 필히 필요함을 알게 되었다. 그리고 코드 수정에도 용이하다. JK에게 칭찬받음 호호:) 

	2. 생성자는 꼭 하나만 있을 필요는 없다.  
		: LadderGameInfo에서 입력받은 그대로의 사용자명 String과 배열로 만든 사용자명, 그리고 사다리의 높이를 가지고 초기화를 하는 생성자를 만들었다. 데이터를 넘겨주는 게 String일 때도 있고, 배열 Data일 때도 있기 때문에 어느 하나는 빈 데이터지만 일단 넘겨줘야해서 비효율적이었다. 그럴 땐 생성자를 하나만 고집하지 말고 두 개로 나누자.

