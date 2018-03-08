# # Step7. Container ViewController

> 피드백

String.init(format:) 방식으로 개선하기: https://github.com/dely2p/swift-photoframe/issues/19
<br  />

```
@godrm
이 부분에서 파일 이름을 생성하는 것을 String.init(format:) 방식으로 개선해보세요.
```
<br  />

> 알게 된 것

이미지 파일 이름이 숫자인데 한 자리 일 때는 앞에 0이 붙게 된다. (ex, 01, 02, 14, 15 ) <br  />
그래서 삼항연산자로 10보다 작으면 0을 붙이고, 아니면 그대로 이미지 이름으로 설정하도록 만들었었다.<br  />
swift에서는 String.init(format:)이 있다는 사실을 알고 적용해서 개선하니 코드가 보다 간결해졌다.<br  />
<br  />
기존 코드

```
@IBAction func nextImageButtonTouched(_ sender: Any) {
    let randomNumber: UInt32 = arc4random_uniform(22) + 1;
    self.photoImageView.image = UIImage(named: randomNumber < 10 ? "0\(randomNumber).jpg" : "\(randomNumber).jpg")
}
```

개선한 코드

```
@IBAction func nextImageButtonTouched(_ sender: Any) {
    let randomNumber: UInt32 = arc4random_uniform(22) + 1;
    self.photoImageView.image = UIImage(named: String.init(format: "%02d.jpg", randomNumber))
}
```
