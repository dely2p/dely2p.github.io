# # Step2. 함수 역할 분리

- 개발한 것(배운 것)

	#####1. 사다리 게임 함수 분리 및 depth 줄이기

	: step2의 과제에서는 기존에 만들었던 사다리 게임의 method가 1가지 일만 하도록 만들고, depth를 2단계에서 1단계로 줄여야 했다. 또한 else를 쓰지 말라고 했다.  

	아래와 같이 메소드 분리를 해보았다.  

	```swift
func prompt(){}
func printLadder(numberOfPlayer: String, heightForLadder: String){}
func printLadderBar(numberOfPlayer: String){}
func printLadderStep(index: Int){}
func makeRandomValue() -> Bool{}
```
	처음에 사용자로부터 입력을 받는 prompt()를 만들고, 사다리를 출력하는 printLadder()를 만들었다. 그리고는 사다리의 가로(printLadderBar())와 세로(printLadderStep())를 각 메소드에서 출력하도록 연결해두었다. 마지막으로 랜덤값을 만들어내는 makeRandomValue()를 만들어서 랜덤값이 필요할 때마다 사용할 수 있도록 해두었다  


	메소드 분리를 하니 조금 깔끔해보였다. 메소드를 타고 타고 for문을 도는 것이 조금 마음에 걸렸지만 메소드 분리를 위해서는 어쩔 수 없었다.  


	```swift
	import Foundation
	
	func prompt(){
	    print("참여할 사람은 몇 명 인가요?")
	    let numberOfPlayer = readLine()
	    
	    print("최대 사다리 높이는 몇 개인가요?")
	    let heightForLadder = readLine()
	    
	    printLadder(numberOfPlayer: numberOfPlayer!, heightForLadder: heightForLadder!)
	}
	
	func printLadder(numberOfPlayer: String, heightForLadder: String){
	    for _ in 0..<Int(heightForLadder)! {
	        printLadderBar(numberOfPlayer: numberOfPlayer)
	        print()
	    }
	}
	
	func printLadderBar(numberOfPlayer: String){
	    for index in 0..<Int(numberOfPlayer)! {
	        printLadderStep(index: index)
	        print("|", terminator: "")
	    }
	}
	
	func printLadderStep(index: Int){
	    let isPrintStep = makeRandomValue()
	    if isPrintStep && index > 0 {
	        print(" ", terminator: "")
	    }else if !isPrintStep && index > 0 {
	        print("-", terminator: "")
	    }
	}
	
	func makeRandomValue() -> Bool {
	    let randomValue = arc4random_uniform(2)
	    var isPrintStep: Bool = false
	    if randomValue == 0 {
	        isPrintStep = false
	    }else{
	        isPrintStep = true
	    }
	    return isPrintStep
	}
	prompt()
	``` 
  
- 피드백

	https://github.com/dely2p/swift-laddergame/issues/2


- 알게 된 것

	1. prompt() 함수에서 printLadder() 함수 분리하기<br  />
: prompt() 함수 이름의 의미가 입력받기만 뜻하는 것 같은데 사다리 출력까지 같이 하고 있기 때문에 main()을 두어서 prompt(), printLadder()을 따로 분리했다.

	```swift
func main(){
    let inputValue = prompt()
    printLadder(numberOfPlayer: inputValue.numberOfPlayer, heightForLadder: inputValue.heightForLadder)
}
```

	2. Boolean 값 바로 return  
: makeRandomValue()에서 boolean값을 바로 return 하면 되는데 굳이 isPrintStep 변수를 두었다. 나름 가독성 좋은 코드를 만들고자 하는 욕심이었던 듯 하나 필요없는 코드는 쓰지않는 게 좋다.