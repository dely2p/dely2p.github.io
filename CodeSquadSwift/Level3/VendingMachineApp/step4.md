# # Step4. 싱글톤 모델

> 개발한 것(배운 것)

### 1. 싱글톤(singleton)

: VendingMachineApp step4에서는 싱글톤을 이용해서 vendingMachine을 한 번만 생성하고 AppDelegate와 Delegate에서 사용하는 그 인스턴스를 사용하도록 만들었다.

기존에 AppDelegate에서 생성하고, 언아카이빙 할 때 생성하던 것을 좀 더 효율적으로 바꿀 수 있었다. 

VendingMachineApp/VendingMachineApp/Model/VendingMachine.swift

```swift
private static var vendingMachine = VendingMachine()
private override init() {
	super.init()
}
```

<br  />
### 2. 싱글톤 인스턴스 get & set

: VendingMachine에서 생성한 인스턴스를 AppDelegate와 ViewController에서 사용하고, 또 바뀐 데이터로 저장해두기 위해서는 VendingMachine에 computed property가 필요했다.<br  />
swift 특성상 get, set을 사용하는 대신 static function을 사용하기로 했고 sharedInstance(), storedInstance() method를 만들었다.

```swift

static func sharedInstance() -> VendingMachine {
	return vendingMachine
}
    
static func storedInstance(_ vendingMachine: VendingMachine) {
	self.vendingMachine = vendingMachine
}
```

<br  />
> 피드백

https://github.com/dely2p/swift-vendingmachineapp/issues/22<br  />
https://github.com/dely2p/swift-vendingmachineapp/issues/23<br  />
https://github.com/dely2p/swift-vendingmachineapp/issues/24<br  />
https://github.com/dely2p/swift-vendingmachineapp/issues/25<br  />
https://github.com/dely2p/swift-vendingmachineapp/issues/26<br  />
https://github.com/dely2p/swift-vendingmachineapp/issues/27<br  />
https://github.com/dely2p/swift-vendingmachineapp/issues/28<br  />
https://github.com/dely2p/swift-vendingmachineapp/issues/29<br  />

<br  />
> 알게 된 것

1. windows 객체의 필요?<br />
: AppDelegate에는 `var window: UIWindow?`가 있는데 이를 지우게 되면 검은색 화면으로 뜨게 된다.(본인은 왠지 필요없어보여 지움;;) AppDelegate에서 window 참조형으로 쓰이기 때문에 꼭 필요하다.


2. 싱글톤 객체를 바로 호출하기<br  />
: AppDelegate의 shared() 대신 VendingMachine의 storedInstance()으로 직접 인스턴스를 사용한다.


3. applicationWillResignActive, applicationDidEnterBackground, applicationWillTerminate 모두가 setUserDefault()를 호출해야 하는가?<br  />
: applicationWillResignActive (홈 버튼을 눌러서 앱이 활성화에서 비활성화 되었을 때), applicationDidEnterBackground (앱이 백그라운드 상태일 때), applicationWillTerminate (앱이 종료될 때) 각각 아카이빙이 필요한 것이 아니라 앱이 백그라운드 상태일 때만 써주어도 된다. 또한 applicationWillTerminate는 아름답게 앱이 종료될 때만 호출된다.(강제종료는 호출 안된다.)

4. self.vendingMachine를 매개변수로 접근하는 부분<br  />
: ViewController에서 vendingMachine이 전역변수로 이미 선언되어 있기 때문에 매개변수로 접근하는 것을 수정했다.

5. 싱글톤으로 직접 접근하기<br  />
: ViewController에서 싱글톤 패턴을 적용한 storedInstance() 메소드를 사용하여 vendingMachine에 직접 접근하도록 개선했다.

6. updateCountOfEachBeverage() 매개변수 없애기<br  />
: 싱글톤을 적용했기 때문에 self.vendingMachine이 아닌 vendingMachine으로 직접 접근이 가능하다.


7. applicationWillResignActive와 applicationDidEnterBackground 차이<br  />
: applicationDidEnterBackground()에만 setUserDefault()가 들어가도록 수정했다.

8. vendingMachine 객체에 의존하지 않도록 만들기<br  />
: Vending이라는 프로토콜을 두어서 vendingMachine 객체에 의존하지 않도록 만들었다.