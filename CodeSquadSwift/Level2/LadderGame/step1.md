# # Step1. 시작하기

> - 개발한 것(배운 것)

### 1. 간단한 사다리 게임 구현

: n개의 사람과 m개의 사다리 개수를 입력받고, 사다리는 랜덤으로 있거나 없을 수도 있다. 사다리가 있으면 -를 표시하고 없으면 " " 빈공백을 표시하고, 양옆에는 |로 세로를 표시하여 사다리 상태를 화면에 출력한다.


그저 c언어로 과제하듯 편안하게 만들었다. 다만 조금 불편했던 것은 옵셔널 때문에 `!`를 쓰라고 메시지가 뜨는 것이었다. 그래서 step1 코드는 `!`천지ㅎㅎ<br  />
지금 다시 보니 왜 조건문을 저렇게 복잡하게 만들었을까 싶긴한데.. 아마 depth를 줄이고 싶었던 것 같다.

```swift
import Foundation

print("참여할 사람은 몇 명 인가요?")
var personNum = readLine()

print("최대 사다리 높이는 몇 개인가요?")
var ladderHeight = readLine()

for _ in 0..<Int(ladderHeight!)! {
    for j in 0..<Int(personNum!)! {
        print("|", terminator: "")

        let rndNum = arc4random_uniform(2)
        if rndNum == 0 && j < 2 {
            print(" ", terminator: "")
        }else if rndNum == 1 && j < 2 {
            print("-", terminator: "")
        }
    }
    print()
}
``` 

<br  />
> - 피드백

https://github.com/dely2p/swift-laddergame/issues/1<br  />


<br  />
> - 알게 된 것

1. 변수명 개선하기
: swift에서는 변수의 의미가 명확한 것을 중시한다는 것을 배웠다. 기존에 c언어나 java에서는 변수명을 축약해서 쓰기도 하고, for문에서 선언되는 index는 i, j, k로 쓰는 것이 흔했는데 swift는 그러면 안되나보다. 흑ㅠㅠ