# # Step3. 함수 역할 분리

> 개발한 것(배운 것)

### 1. 객체를 별도 파일에 생성하면서 main.swift 에서는 분리한 객체들 인스턴스끼리 조합하기

: step3에서는 하나의 파일에 메소드를 쭉 나열하듯

<br  />
> 피드백

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

<br  />
> 알게 된 것

1. 접근제어 지정하기<br  />
: private에 익숙치 않았다. 그냥 데이터는 바로 접근해서 쓰는 것에 익숙해서;; 나만 쓰는 프로그램이 아닌 다른 사람들도 쓰는 프로그램을 만들기 위해서는 접근 제어를 위해 직접 접근하기보단 메소드를 통해서 가져오도록 해야 한다.

2. 입력 값에 대한 예외처리 하기<br  />
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

<br  />
