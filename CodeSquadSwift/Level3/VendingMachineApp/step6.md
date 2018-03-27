# # Step6. 구매목록 View 코드

> 개발한 것(배운 것)

### 1. self.view.addSubView()
: VendingMachineApp step6에서는 self.view.addSubView()를 이용하여 구매한 음료 이미지를 하단에 출력하도록 만들었다. 

```swift   
let imageView = ImageViewMaker.makeImageView(imageX: imageX)
imageView.image = image
self.view.addSubview(imageView)
self.imageX += 50

```

### 2. Class Name을 이용하여 image 파일명 가져오기
: Class Name과 image 파일명이 같은 것을 이용하여 구매한 이미지를 가져올 수 있도록 만들었다.  
`String(describing: type(of: self))`으로 (self==Beverage(cf, StrawberryMilk)) 클래스명을 가져오고, `.jpg`를 붙여서 String을 return 해주었다.  
그리고 `UIImage(named: imageName)`로 이미지를 가져 올 수 있다. 

```swift
let imageName = String(describing: beverage.bringImageName)
guard let image = UIImage(named: imageName) else {
    return
}
```

```swift
protocol ImageMapper {
    var bringImageName: String { get }
}

extension ImageMapper {
    var bringImageName: String {
        let name = String(describing: type(of: self))
        let result = name + ".jpg"
        return result
    }
}
```

> 피드백

https://github.com/dely2p/swift-vendingmachineapp/issues/40  
https://github.com/dely2p/swift-vendingmachineapp/issues/41  
https://github.com/dely2p/swift-vendingmachineapp/issues/42  
https://github.com/dely2p/swift-vendingmachineapp/issues/43  
https://github.com/dely2p/swift-vendingmachineapp/issues/44  
https://github.com/dely2p/swift-vendingmachineapp/issues/45  
https://github.com/dely2p/swift-vendingmachineapp/issues/46  
https://github.com/dely2p/swift-vendingmachineapp/issues/47  
https://github.com/dely2p/swift-vendingmachineapp/issues/48  
https://github.com/dely2p/swift-vendingmachineapp/issues/49  


> 알게 된 것

### 1. 하드코딩되어 있는 숫자 개선하기
: Beverage price를 넣은 struct를 만들어서 클래스 생성 시 가져다가 쓸 수 있도록 개선했다.

```swift
self.init(brand: "", weight: 0, price: 1200, name: "", manufactureDate: Date(), cocoaPower: 1)
```
↓ 코드 개선

```swift
self.init(brand: "", weight: 0, price: BeveragePrice.chocoMilk, name: "", manufactureDate: Date(), cocoaPower: 1.1)
```

```swift
struct BeveragePrice {
    static let strawberryMilk = 1500
    static let bananaMilk = 1000
    static let chocoMilk = 1200
    static let sprite = 2000
    static let fanta = 800
    static let coke = 800
    static let georgia = 1000
    static let kantata = 1300
    static let top = 1500
}
```

### 2. 클래스 파일명으로 이미지 파일 이름을 바꾸기
: 

### 3. 구매 실패 시 에러메시지 띄우기

### 4. ViewController 변수 접근제어 수정하기

### 5. 왜 vending 변수를 새로 바꾸는거죠?

### 6. imageOfMenu 화면 설정하는 코드 하위 모듈로 감추도록 개선하기

### 7. viewDidLoad 내 여러 기능들 메소드로 분리하기

### 8. printPurchaseProducts() method 함수명 수정하기

### 9. 이전코드 흔적인 Formatter 삭제하기

### 10. 원 단위 같은건 안 붙이나요?