# # Step3. 앱 생명주기와 객체 저장

> 개발한 것(배운 것)

<br  />
### 1. NSObject와 NSCoding 프로토콜**

: VendingMachineApp step3에서는 앱의 데이터를 저장하기 위해 아카이빙을 하고 저장한 데이터를 가져오기 위해 언아카빙을 하는 것을 만들었다. 앱 생명주기에 맞춰서 그 코드들을 넣어줬고 각 모델마다 NSObject와 NSCoding 프로토콜을 넣고 encode() init() 코드를 구현해주었다.

사실 Codable을 사용해보려 했지만 데이터를 Json형식이나 다른 형태로 바꿔주는 데 더 적합한 프로토콜 같아서.. 많은 중복 작업이 있었지만 열심히 NSObject와 NSCoding 프로토콜로 만들었다. 

```swift
class VendingMachine: NSObject, NSCoding {
	required init?(coder aDecoder: NSCoder) {
	        coins = aDecoder.decodeInteger(forKey: "coins")
	        inventoryBox = (aDecoder.decodeObject(forKey: "inventoryBox") as? InventoryBox)!
	        purchaseProductHistory = (aDecoder.decodeObject(forKey: "purchaseProductHistory") as? PurchaseProductHistory)!
	        super.init()
	    }
	    
	    func encode(with aCoder: NSCoder) {
	        aCoder.encode(coins, forKey: "coins")
	        aCoder.encode(inventoryBox, forKey: "inventoryBox")
	        aCoder.encode(purchaseProductHistory, forKey: "purchaseProductHistory")
	    }
}
```

<br  />
### 2. [ObjectIdentifier:[Beverage]] encoding, decoding하기

: encode, decode할 때 문제가 생겼다. 모든 type의 인코딩, 디코딩을 지원하고 있지 않아서 raw type인 ObjectIdentifier은 인코딩, 디코딩을 할 수 없기 때문이었다.<br  />
하지만 나는 뭔가 extends 하거나 다른 방법이 있을 것이라는 생각에 하루종일 구글링도 해보고 NSStringToClass()와 NSClassToString()도 사용해보고 여러가지 방법을 생각해봤지만 다 안됐다..ㅠㅠ

앞서 이 과정을 거친 Jack이 이전에 배열을 하나 만들어 value만 넣어서 사용했다고 해서 그 방법을 사용하려 했는데 문제는 ObjectIdentifier인 key가 없는데 value를 어떻게 구분하는가 였다. 

알고보니 value로 담고 있는 [Beverage]는 `ObjectIdentifier(type(of: Beverage))`를 하면 다시 key값을 알 수 있어서 [ObjectIdentifier:[Beverage]]를 생성할 수 있던 것이었다. 그래서 그 방법대로 만들어서 해결할 수 있었다.

<br  />
### 3. Archive & UnArchive 그리고 UserDefault

: 처음엔 Archive와 UserDefault가 같은 레벨의 저장방법이라고 생각했다. 그래서 개념도 못잡고 한참 헤맸는데 JK에게 질문하여 물어보니 Archive가 저장하는 것인데 그 방법 중에 UserDefault도 있고, mdb도 있고, file도 있고 그런 것이었다. 

그래서 다시 방향을 잡고 앱 생명주기에 맞춰서 코드를 만들었다. 그런데 구글링을 해서 찾은 코드들은 예전 코드가 많아서 친절한 xCode가 바꾸라고 말해줬다.

```
//Archive
let data = NSKeyedArchiver.archivedData(withRootObject: vendingMachine)
        UserDefaults.standard.set(data, forKey: "vendingMachine")
 
//unArchive
if let data = UserDefaults.standard.data(forKey: "vendingMachine") {
            vendingMachine = (NSKeyedUnarchiver.unarchiveObject(with: data) as? VendingMachine)!
        }
```

<br  />
### 4. AppDelegate와 ViewController의 vendingMachine instance 데이터 값 불일치

: 사실 진짜 어려움은 여기부터였다. 아무리 음료데이터를 추가해서 아카이빙해도 다시 앱을 켜면 초기 데이터로 나왔다. 코드마다 breakpoint를 걸어서 data의 행적(?)을 찾아봤는데 encode를 할 때 분명 값이 VendingMachine을 거쳐 InventoryBox에 잘 들어가는 것까지는 확인을 했는데 그 다음 코드 순서인 encode를 할 때 들어가는 vendingMachine의 InventoryBox에는 값이 없던 것이었다.

그래서 또다시 JK에게 질문을 했다. 알고보니 ViewController에서 AppDelegate에 접근해서 가져온 vendingMachine이 사용자의 데이터 입력을 받아서 수정되었는데, AppDelegate에서 enecode할 때는 초기의 vendingMachine을 계속 가지고 있던 것이었다.

<img src="./img/vendingMachineNoData.png" height="80%" width="60%">

```
let appDelegate = UIApplication.shared.delegate as? AppDelegate
vendingMachine = appDelegate?.vendingMachine

```

```
var vendingMachine = VendingMachine
```

<br  />
> 피드백

https://github.com/dely2p/swift-vendingmachineapp/issues/10<br  />
https://github.com/dely2p/swift-vendingmachineapp/issues/11<br  />
https://github.com/dely2p/swift-vendingmachineapp/issues/12<br  />

<br  />
1. 음료수 type을 넣었던 enum을 기존 VendingMachine 코드를 사용하여 수정하기<br />
2. countOfEachBeverage 배열도 기존 코드 써서 수정하기
<br  />
3. IBAction 반복되는 코드 한꺼번에 처리하기

```swift
VendingMachineApp/VendingMachineApp/ViewController.swift
	
+    
+    @IBAction func addMenu9(_ sender: Any) {
+        alertCountOfBeverage(type: TypeOf.kantanta)
+    }
```

```swift
@godrm
여기 액션들도 반복되는 코드처럼 보이는데 한꺼번에 처리하려면 어떻게 해야할까 고민해보세요.
```

<br  />
> 알게 된 것

1. IBOutlet collection 뿐만 아니라 IBAction도 동일하게 여러개의 버튼에 한꺼번에 접근할 수 있었다. (storyboard에서 각 버튼의 태그를 지정해준 후 for문에서 sender.tag로 눌러진 버튼을 구분할 수 있음)

```
@IBOutlet var addNumberOfMenu: [UIButton]!
@IBAction func addBeverage(sender: UIButton) {
    var type = TypeOf.otherBeverage
    for button in addNumberOfMenu where button.tag == sender.tag {
        type = vendingMachine.typeSelector(tag: button.tag)
    }
    alertCountOfBeverage(type: type)
}
```
