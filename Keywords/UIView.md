# UIView

`UIView`는 iOS 앱에서 사용자 인터페이스를 만들고 조작하는 데 필수적인 클래스입니다.

[UIKit]() 프레임워크에 속해 있으며, 화면에 표시되는 모든 것들은 `UIView`나 그 하위 클래스의 인스턴스입니다.<br/>
`UIView`는 화면의 특정 영역을 캡슐화하고, 이 영역에서는 그림을 그릴 수 있고, 이벤트를 처리하며, 애니메이션을 구현할 수 있습니다.<br/>
또한, 다른 뷰를 포함할 수 있으므로 뷰 계층 구조를 만들 수 있습니다.<br/>

`UIView` 클래스는 다음과 같은 주요 책임을 가집니다.<br/>

1. 뷰와 하위 뷰의 렌더링: `UIView`는 자체의 `draw(_:)` 메소드를 통해 그려집니다. 이 메소드는 필요에 따라 재정의할 수 있으며, 주로 그리기를 수행해야 하는 커스텀 뷰에서 사용됩니다. 또한, `UIView`는 자신의 하위 뷰를 렌더링하는 작업도 수행합니다.

2. 이벤트 처리: `UIView`는 터치, 제스처 등의 이벤트를 처리하는 메소드를 제공합니다. 이를 통해 사용자와의 상호작용을 구현할 수 있습니다.

3. 레이아웃과 크기 조정: `UIView`는 `layoutSubviews()` 메소드를 통해 자신과 하위 뷰의 레이아웃을 관리합니다. 또한, `autoresizingMask` 또는 Auto Layout을 사용하여 뷰의 크기와 위치를 동적으로 조정할 수 있습니다.

4. 애니메이션: `UIView`는 애니메이션 효과를 적용할 수 있는 메소드를 제공합니다. 이를 통해 뷰의 위치 이동, 크기 변경, 페이드 인/아웃 등 다양한 효과를 구현할 수 있습니다.

[UIKit]()에는 `UIView`의 여러 하위 클래스가 있으며, 이를 통해 버튼(`UIButton`), 레이블(`UILabel`), 이미지 뷰(`UIImageView`), 스크롤 뷰(`UIScrollView`), 테이블 뷰(`UITableView`) 등 다양한 UI 요소를 생성하고 사용할 수 있습니다. 이러한 요소들은 모두 `UIView`의 기본 기능을 상속받아 특화된 기능을 추가로 제공합니다.

# 연관 키워드

[UIKit]()

# 공식 문서
https://developer.apple.com/documentation/uikit
