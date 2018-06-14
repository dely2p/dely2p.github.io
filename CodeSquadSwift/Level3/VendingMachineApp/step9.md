# # Step9. 마무리하기

> 개발한 것(배운 것)

### 1. Touch event
```swift
override func touchesBegan(_ touches: Set<UITouch>, with event: UIEvent?) {
        guard let touch = touches.first else {
            return
        }
        let location = touch.location(in: self)
        if pow((centerOfGraph.x - location.x), 2) + pow((centerOfGraph.y - location.y), 2) < pow(radiusOfGraph, 2) {
            isTouched = true
            setNeedsDisplay()
        }
    }
```
: touchesBegan() ,touchesMoved(), touchesEnded() 메소드 안에서 touches 매개변수를 통해 터치 된 부분의 좌표를 알 수 있다. 내가 사용한 속성값은 touches.first 인데 멀티 터치 값도 가져올 수 있는 것 같다.  


### 2. Shake motion
```swift
override func motionEnded(_ motion: UIEventSubtype, with event: UIEvent?) {
        if motion == .motionShake {
            pieChartView.drawByShake()
        }
    }
```
: 아이폰을 흔들면 반응하는 모션 메소드이다. 물론 모션은 다양한 것들을 정해둘 수 있다. 이번 프로젝트에서는 아이폰을 흔들면 파이 그래프의 크기를 다시 초기화 하도록 만드는 것이었다.


> 피드백

https://github.com/dely2p/swift-vendingmachineapp/issues/64  
https://github.com/dely2p/swift-vendingmachineapp/issues/65  
https://github.com/dely2p/swift-vendingmachineapp/issues/66  

> 알게 된 것

### 1. extension 타입조건 직접 넣기
: extension으로 Array를 확장하여 shuffle()을 구현했다.  
Array처럼 swift type 같은 경우는 where절을 사용하여 타입조건을 직접 넣고, 내가 만든 protocol 같은 경우는 :(콜론)을 붙여서 타입조건을 넣어 줄 수 있다.(@Min 의 구두 설명 참조)

```swift
extension Array where Element == UIColor {
    mutating func shuffle(_ number: Int) -> [UIColor] {
        var list = self
        for index in list.indices {
            if index > number { break }
            let random = Int(arc4random_uniform(UInt32(number)))
            list.swapAt(index, random)
        }
        return list
    }
}
```