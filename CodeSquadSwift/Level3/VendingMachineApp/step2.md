# # Step2. MVC 패턴

> 개발한 것(배운 것)

: VendingMachineApp step2에서는 storyboard에서 앱 뷰를 만들고 버튼과 라벨을 ViewController와 연결해서 코드를 작성하여 기능을 만드는 것이다. 안드로이드 앱 개발과는 달리 control key와 마우스로 해당 UI를 끌어다가 코드 작성 화면에 놓으면 연결되기 때문에 참 쉽다.<br  />
그래서 내가 만든 storyboard는 다음과 같다.<br  /><br  />
<img src="./img/step2.png" width="80%" height="80%" align="center"><br  /><br  />


1. alert
<br  />

: alert는 형식이 정해져있어서 형식대로만 작성하면 되는 것 같다.<br  /><br  />
<img src="./img/alert.png" width="80%" height="80%" align="center"><br  />
```swift
func alertCountOfBeverage(type: TypeOf) {
        let title = "추가"
        let message = "추가 할 재고 갯수를 입력하세요."
        let alert = UIAlertController(title: title, message: message, preferredStyle: .alert)
        let cancel = UIAlertAction(title: "취소", style: .cancel)
        let ok = UIAlertAction(title: "확인", style: .default) {(_) in
            if let inputValue = alert.textFields?[0] {
                guard let numberOf = Int(inputValue.text ?? "0") else {
                    return
                }
                let beverageName = self.vendingMachine.choiceBeverageData(menuType: type)
                self.vendingMachine.addInInventory(beverageName: beverageName, number: numberOf)
                self.updateCountOfEachBeverage(vendingMachine: self.vendingMachine)
            }
        }
        alert.addAction(cancel)
        alert.addAction(ok)
        alert.addTextField(configurationHandler: {(text) in
            text.placeholder = "갯수입력"
        })
        self.present(alert, animated: true)
    }
```
<br  /><br  />
2. IBOutlet Collection<br  />
: 여러개의 버튼을 한꺼번에 순서대로 정의하고 싶을 때 사용할 수 있다.
실제로 `@IBOutlet var countOfMenu: [UILabel]!` 이러한 형태로 만들어지는데 for문을 사용하여 배열처럼 해당 라벨, 이미지 등등에 접근할 수 있다.
```swift
@IBOutlet var imageOfMenu: [UIImageView]!
for (index, menu) in TypeOf.kind.enumerated() {
            countOfMenu[index].text = String(vendingMachine.beverageNumberOf(menuType: menu))
        }
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
