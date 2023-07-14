# CGRect

`CGRect`는 **Core Graphics Rectangle**의 약자로, 사각형의 위치와 크기를 나타내는 구조체입니다.<br/>
즉, 이는 2D 그래픽 시스템에서 사각형 영역을 표현하는 데 사용되는 데이터 타입입니다.

`CGRect`는 네 가지 속성을 가지고 있습니다.

- `origin`: 사각형의 왼쪽 하단 꼭짓점을 나타내는 `CGPoint` 타입의 속성입니다.<br/> `CGPoint`는 2차원 좌표 시스템에서의 점을 표현합니다.
- `size`: 사각형의 너비와 높이를 나타내는 `CGSize` 타입의 속성입니다.
- `width`: 사각형의 너비를 나타내는 속성입니다. 이는 `size.width`와 동일한 값을 가집니다.
- `height`: 사각형의 높이를 나타내는 속성입니다. 이는 `size.height`와 동일한 값을 가집니다.

# 궁금했던 점 (GPT 4.0)

**Mojito:**<br/>
실제 CGRect 구현 코드는 어떻게 되어 있나요?

**GPT4.0:**<br/>
CGRect(CGPoint, CGSize 도 동등)는 실제로 [Core Graphics](https://developer.apple.com/documentation/coregraphics)라는 C 기반의 프레임워크에 선언되어 있습니다.

[Core Graphics](https://developer.apple.com/documentation/coregraphics) 소스 코드는 Apple에 의해 관리되며, 공개되지 않았습니다.<br/>
그러나 Apple은 [Core Graphics](https://developer.apple.com/documentation/coregraphics)에 대한 상세한 문서와 API 가이드를 제공하고 있으므로, 이를 통해 라이브러리의 작동 방식을 이해하는 데 도움이 됩니다.

추가적으로 원래 Objective-C와 C 기반의 [Core Graphics](https://developer.apple.com/documentation/coregraphics)에서 정의된 데이터 타입이지만, Swift와 [Core Graphics](https://developer.apple.com/documentation/coregraphics) 사이의 [브리징](https://developer.apple.com/documentation/swift/importing-objective-c-into-swift) 덕분에 Swift에서도 자유롭게 사용할 수 있습니다.

# 연관 키워드

[CGSize]()<br/>
[CGPoint]()<br/>
