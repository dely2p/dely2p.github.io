# # Step5. ViewController 프로그래밍

> 피드백

yellowVC.dismiss() vs self.dismiss() 차이점: https://github.com/dely2p/swift-photoframe/issues/13
<br  />

```
ViewController에서 yellowVC.dismiss() 하는 것과
YellowViewController에서 self.dismiss() 하는 것의 차이점이 뭘까요?
둘 다 동작할까요?
```
<br  />

> 알게 된 것

1. dismiss()는 아이폰 앱에서 띄운 화면을 닫을 때 쓰인다.
<br  />
보통 현재화면에서 '닫기' 버튼을 누르면 화면이 사라지고, 코드에서도 현재화면의 버튼에 해당하는 메소드에서 self.dismiss()를 호출하기 때문에 '스스로 닫는다'라고 생각할 수 있지만.. 사실 알고보면 현재 화면을 닫는 주체는 **이전에 현재 화면을 띄운 뷰컨트롤러**이다.<br  /><br  />
그렇기 때문에  self.dismiss()라는 표현은 정확하게 말하면 self.presentingViewController?.dismiss()와 같은 의미이다.<br  />
이는 "나(현재화면) 사라져!"라기 보단, "나(현재 화면)를 이전에 띄워줬던 뷰컨트롤러야~ 이제 지금 띄워져 있는 것(현재 화면)을 사라지게 해줘~"이다.<br  /><br  />
그렇다면 피드백의 질문처럼 AViewController -> BViewController인 구조를 가진 앱이 있을 때,<br  />
❶AViewController에서 BViewController.dismiss()를 호출하는 것과 ❷BViewController에서 self.dismiss()를 호출하는 것은 결국 같은 것 아닐까?<br  /><br  />
그 답은<br  />
'현재 화면이 사라진다는 동작은 같더라도, 호출하는 주체가 다르기 때문에 화면이 사라지고 난 직후에 **complete 핸들러를 처리**하는 과정은 다르다.'이다.<br  /><br  />
❶의 경우(=self.presentedViewController?.dismiss())는 AViewController에서 BViewController의 dismiss()를 호출하기 때문에 complete 핸들러 처리를 하기 어렵고,<br  />
❷의 경우(=self.presentingViewController?.dismiss())는 BViewController에서 self의 dismiss()를 호출하기 때문에 complete 핸들러 처리를 할 수 있다. (실제로 dismiss()의 매개변수로도 알 수 있다.)<br  /><br  />
직접 확인 해보기 위해 dismiss(animated: true, completion: nil)의 매개변수 completion에 클로저로 print()문을 작성해보았다.<br  />
```
self.dismiss(animated: true, completion: {(print("close pink View"))})
```
BViewController의 viewWillDisappear(), viewDidDisappear()와 AViewController의 viewWillAppear(), viewDidAppear()를 작성하여 출력을 비교해보니

```
1.bVC의 viewWillDisappear()
2.aVC의 viewDidAppear()
3.bVC의 viewDidDisappear()
4.completion 클로저 호출
```

순서로 동작하는 것을 볼 수 있었다.<br  /><br  />

2. **presentedViewController** vs **presentingViewController**
<br  />
presentedViewController : 자신이 호출한 뷰컨트롤러 저장<br  />
presentingViewController: 자신을 호출한 뷰컨트롤러 저장<br  />
