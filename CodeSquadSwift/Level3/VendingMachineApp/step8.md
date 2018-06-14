# # Step8. 코어 그래픽스(Core Graphics)

> 개발한 것(배운 것)

### 1. PieGraphview클래스에 구매이력 넘겨주기

ManagerViewController.swift

```swift
func receiveData() -> [String: Int] {
    guard let vendingMachine = vendingMachine else { return [:] }
    let data = vendingMachine.showPurchaseProductHistory()
    var beverage = [String: Int]()
    let listOfBeveragePurchases = data.map({$0.purchaseBeverage}) //[Beverage]
    var name: String
    
    for product in listOfBeveragePurchases {
        name = String(describing: type(of: product))
        if !beverage.keys.contains(name) {
            beverage[name] = 0
        }
        beverage[name]! += 1
    }
    return beverage
}
```
PieGraphView.swift

```swift
var pieDrawable: PieDrawable? {
    didSet {
        guard let data = pieDrawable?.receiveData() else {
            return
        }
        self.beverage = data
    }
}
```

: ManagerViewController에서 Data를 준비해놓고, PieGraphView에서 프로퍼티 옵저버를 사용하여 데이터를 가져올 수 있다. (PieDrawble 프로톸콜 사용)

### 2. 파이그래프(Pie graph) 그리기

```swift
private func drawPieGraph(pieData: DataOfPieGraph) {
    let point = calculatePoint(center: centerOfGraph, angle: pieData.startAngle, radius: radiusOfGraph)
    pieData.path.addLine(to: point)
    pieData.path.addArc(withCenter: centerOfGraph, radius: radiusOfGraph, startAngle: pieData.startAngle, endAngle: pieData.endAngle, clockwise: true)
    pieData.path.addLine(to: centerOfGraph)
    pieData.path.fill()
    pieData.path.close()
}
```
: UIBezierPath를 이용하여 파이그래프를 그리기 위해서는 점, 선, 면을 잘 활용해야 했다. 먼저 중점으로 이동하여 원 위의 점을 계산하여서 두 점 사이를 선으로 잇는다. 그리고는 각도를 계산하고 원의 호를 그리도록 한다.
그 이후에는 원의 중점으로 선을 그린다.  
이제 그 안에 색을 칠 할 수 있다. 조금이라도 닫힌 선이 아니라면 subView 전체가 색이 칠해진 것을 볼 수 있다.ㅠㅠ


### 3. 파이그래프 위에 글자 넣기
```swift
private func drawTextOnPieGraph(pieData: DataOfPieGraph) {
    let textPoint = calculateTextPoint(center: centerOfGraph, startAngle: pieData.startAngle, endAngle: pieData.endAngle, radius: radiusOfGraph)
    let textToRender: NSString = pieData.product.key as NSString
    var renderRect = CGRect(origin: .zero, size: textToRender.size(withAttributes: textAttributes))
    renderRect.origin = textPoint
    textToRender.draw(in: renderRect, withAttributes: textAttributes)
}
```

```swift
private lazy var textAttributes: [NSAttributedStringKey: Any] = {
    let myShadow = NSShadow()
    myShadow.shadowBlurRadius = 3
    myShadow.shadowOffset = CGSize(width: 3, height: 3)
    myShadow.shadowColor = UIColor.gray
    return [NSAttributedStringKey.foregroundColor: UIColor.white, NSAttributedStringKey.shadow: myShadow, NSAttributedStringKey.font: UIFont(name: "Helvetica-Bold", size: radiusOfGraph - Constants.fontSize)!]
}()
```

:그래프 위에 글자를 넣기 위해서는 그래프를 그리고 색을 칠한 후에 글자를 출력하도록 만들어 주어야 한다. 이때 String이 아니라 NSString을 사용하게 된다. 그리고 글자의 속성도 만들어주게 되는데, 나는 그림자와 폰트, 사이즈를 정해주었다. 속성은 `[NSAttributedStringKey: Any]` type으로 정해줄 수 있다.


> 피드백

https://github.com/dely2p/swift-vendingmachineapp/issues/59  
https://github.com/dely2p/swift-vendingmachineapp/issues/60  
https://github.com/dely2p/swift-vendingmachineapp/issues/61  


> 알게 된 것

### 1. let 상수를 인스턴스 상수로 표현하기

: 기존에 draw() 메소드 안에서 centerOfGraph와 sizeOfView 상수를 선언하여 사용했다. 그런데 JK가 draw 메소드가 드로잉 엔진에 따라 엄청 자주 불리기 때문에 인스턴스 상수로 처리하는 것이 더 좋다고 피드백을 주셔서 개선하게 되었다.  
그런데 중점과 subview의 사이즈를 계산하는 것이다보니 bounds를 참조해야만해서 computed property를 사용하게 되었다.  
 
사실 코드를 작성하다가 중간에 문제가 생겼었는데, centerOfGraph: CGPoint{}로 작성한다는 것이 centerOfGraph = CGPoint{} 형태로 작성했다. 후자의 경우 초기화 해버리는 것이기 때문에 bounds에 접근할 수가 없어서 한참 헤매다가 이유를 찾을 수 있었다. (주의 또 주의!)

```swift
private var centerOfGraph: CGPoint {
    return CGPoint(x: bounds.width / 2, y: self.bounds.height / 2)
}
private var sizeOfView: CGFloat {
    return max(bounds.width, bounds.height)
}
```