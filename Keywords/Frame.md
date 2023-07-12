# Frame

`frame`은 UIView의 View가 화면에서 차지하는 공간을 말하며, 좌표 시스템을 기반으로 합니다.<br/>
UIView의 `frame`은 [CGRect]() 타입으로, 사각형의 영역을 정의합니다.<br/>
이는 `origin`과 `size`로 구성됩니다.

예를 들어 다음과 같이 `frame`을 설정할 수 있습니다.

```swift
// 화면의 좌측 상단에서 시작하여 너비와 높이가 각각 100 픽셀인 사각형의 뷰를 생성
let view = UIView()
view.frame = CGRect(x: 0, y: 0, width: 100, height: 100)
```

`frame`은 해당 뷰의 부모 뷰(superview)에 상대적인 위치를 나타냅니다.<br/>
즉, `frame`의 좌표값은 **부모 뷰의 좌측 상단 꼭짓점**을 기준으로 합니다.

# 연관 키워드

[UIView]()<br/>
[CGRect]()<br/>
[CGSize]()<br/>
