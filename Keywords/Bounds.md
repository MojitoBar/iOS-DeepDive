# Bounds

`bounds`는 뷰의 내부 좌표계에서 뷰 자체의 위치와 크기를 나타냅니다.<br/>
[UIView](https://github.com/MojitoBar/iOS-DeepDive/blob/main/Keywords/UIView.md)의 `frame`은 [CGRect](https://github.com/MojitoBar/iOS-DeepDive/blob/main/Keywords/Frame.md) 타입으로, 사각형의 영역을 정의합니다.<br/>
이는 `origin`과 `size`로 구성됩니다.

```swift
// 뷰의 내부 좌표 시스템을 변경하여 컨텐츠가 우측 하단으로 10픽셀 이동하도록 설정하고, 뷰의 내부 너비와 높이를 각각 100으로 설정
let view = UIView()
view.bounds = CGRect(x: 10, y: 10, width: 100, height: 100)
```

가장 중요한 것은 `bounds`는 뷰의 내부 좌표 시스템에 기반을 두고 있다는 점입니다.<br/>
예를 들어, 뷰가 회전하거나 확대/축소되었다면 `bounds`는 이 변경사항을 반영하지 않습니다.<br/>
`bounds`가 뷰의 "자기 관점"에서 뷰의 위치와 크기를 나타내기 때문입니다.

즉, `bounds`는 **자기 자신을 기준**으로 하는 좌표계입니다.

# 연관 키워드

[UIView](https://github.com/MojitoBar/iOS-DeepDive/blob/main/Keywords/UIView.md)<br/>
[CGRect](https://github.com/MojitoBar/iOS-DeepDive/blob/main/Keywords/CGRect.md)<br/>
[CGSize]()<br/>
