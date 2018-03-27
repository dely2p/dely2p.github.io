# # Step7. 구매목록 View 코드

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

### 1. Notification.Name 선언  
: Notification.Name 선언을 해서 사용하면 하드 코딩을 하지 않아도 된다.(더 깔끔한 코드)

```swift
 NotificationCenter.default.post(name: Notification.Name("changeInventoryBox"), object: self)
```

↓ 코드 개선함

```swift
NotificationCenter.default.post(name: Notification.Name.DidResetInventoryBox, object: self)
```
  
### 2. 노티를 받을 때 데이터를 넘겨받고 싶으면?
: NotificationCenter.default.post() 매개변수로 UserInfo를 두어 데이터를 넘겨받을 수 있다.

```swift
let someInfomation: [String: Int] = ["test", 0]
NotificationCenter.default.post(
					name: NSNotification.Name(rawValue: "notificationName"), 
                    object: nil, 
                    userInfo: someInfomation)
)
```

또한 넘겨받은 데이터를 사용할 때는 NSNotification type의 매개변수를 이용하여 데이터를 가져올 수 있다.

```swift
func changeInventoryBox(_ notification: NSNotification){
        if let data = notification.userInfo as Dictionary {
               if let result = data["test"] {
                       print(result) // 0
               }
        }
}
```

참고 문서: https://stackoverflow.com/questions/36910965/how-to-pass-data-using-notificationcentre-in-swift-3-0-and-nsnotificationcenter
https://developer.apple.com/documentation/foundation/nsnotification/1409222-userinfo