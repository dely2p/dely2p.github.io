# # Step5. 관찰자(Observer) 패턴

> 개발한 것(배운 것)

### 1. 관찰자(Observer)패턴
: VendingMachineApp step5에서는 관찰자 패턴을 이용해서 Model의 데이터가 바꼈을 때 이를 알려주고 그에 따른 행동을 할 수 있도록 만들었다.

`옵저버 등록, 호출, Notification.Name 선언, 함수 작성`으로  
코드를 작성하여 Notification을 할 수 있다.

##### 1) 옵저버 등록

```swift
NotificationCenter.default.addObserver(self,
                   selector: #selector(changeInventoryBox),
                   name: Notification.Name.DidResetInventoryBox,
                   object: nil)
```

##### 2) 옵저버 호출

```swift
NotificationCenter.default.post(name: Notification.Name.DidResetInventoryBox, object: self)
```

##### 3) Notification.Name 선언

```swift
extension Notification.Name {
    static let DidResetInventoryBox = Notification.Name("changeInventoryBox")
}
```

##### 4) 함수 작성

```swift
@objc func changeInventoryBox() {
    for (index, menu) in TypeOf.kind.enumerated() {
        countOfMenu[index].text = String(vendingMachine.beverageNumberOf(menuType: menu))
    }
}
```


> 피드백

https://github.com/dely2p/swift-vendingmachineapp/issues/33  
https://github.com/dely2p/swift-vendingmachineapp/issues/34


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