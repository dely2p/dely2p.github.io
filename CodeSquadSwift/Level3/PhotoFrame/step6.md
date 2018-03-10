# # Step6. Container ViewController

> 피드백

https://github.com/dely2p/swift-photoframe/issues/16

1. 여러번 push 한 상태에서 맨 앞으로 pop하는 방법은?
<br  />

```
@godrm
만약 여러번 push를 한 상태에서 pop 할때 맨 마지막 화면이 아니라 마지막 두 개를 pop하려면 어떻게 해야할까요?
맨 앞으로 pop하는 방법은 뭘까요?
```
<br  />

> 알게 된 것

: Navigation Controller에서 여러 개의 뷰가 쌓여있을 때 맨 앞으로 pop하는 방법으로는,<br  />
1. storyboard로 만들기 - Unwind Segue를 구현한다. (원하는 화면에 Unwind를 위한 메소드를 만들어두고 마지막 화면 버튼을 상단 도크바의 Exit에 연결하여 만들어둔 Unwind를 위한 메소드로 설정해둠)

2. 코드로 구현하기 - 이동을 원하는 화면과 첫화면을 Segue로 연결한 후(Identifier에 segue 이름 작성) 뷰컨트롤러에 button IBAction 메소드 안에 코드를 작성하여 맨 앞으로 pop을 할 수 있다.

   1) performSegue()
    
```
self.performSegue(withIdentifier: "unwindToFirst", sender: nil)
```

   2) popToRootViewController()

```
navigationController?.popToRootViewController(animated: false)
```

   3) popToViewController()

```
guard let navi = navigationController?.childViewControllers[0] else {
return
}
navigationController?.popToViewController(navi, animated: false)
```

