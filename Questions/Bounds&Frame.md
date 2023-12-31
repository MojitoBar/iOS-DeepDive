# Bounds와 Frame의 차이점

**Frame**: 이는 상위 뷰의 좌표 시스템에서 뷰의 위치와 크기를 나타내는 [CGRect](https://github.com/MojitoBar/iOS-DeepDive/blob/main/Keywords/CGRect.md)입니다.<br/>
예를 들어, 만약 [UIView](https://github.com/MojitoBar/iOS-DeepDive/blob/main/Keywords/UIView.md)의 [Frame](https://github.com/MojitoBar/iOS-DeepDive/blob/main/Keywords/Frame.md)이 `(x: 50, y: 50, width: 100, height: 100)`이면, 이 뷰는 부모 뷰의 왼쪽 상단 모서리로부터 오른쪽으로 50포인트, 아래로 50포인트 떨어진 위치에 있으며, 뷰의 너비와 높이는 각각 100포인트입니다.

**Bounds**: 이는 뷰의 내부 좌표 시스템에서 뷰의 크기를 나타내는 [CGRect](https://github.com/MojitoBar/iOS-DeepDive/blob/main/Keywords/CGRect.md)입니다. [Bounds](https://github.com/MojitoBar/iOS-DeepDive/blob/main/Keywords/Bounds.md)의 원점은 기본적으로 뷰의 왼쪽 상단 모서리이며, 그 값을 변경하면 뷰의 내부 콘텐츠가 스크롤되는 방식에 영향을 줄 수 있습니다.<br/>
따라서, bounds의 원점이 (0, 0)이 아닌 다른 값으로 설정되면, 뷰의 콘텐츠가 해당 값만큼 오프셋이 발생하게 됩니다.

이 둘의 가장 큰 차이점은, `frame`이 뷰의 외부 위치와 크기를 나타내는 반면, `bounds`는 뷰의 내부 크기를 나타내며, 그 내부에서의 콘텐츠 위치를 제어한다는 것입니다.

이 차이점은 뷰가 **회전**하거나 **변형**될 때 특히 중요해집니다.<br/>
뷰가 회전하면 `frame`은 더 이상 유효하지 않지만, `bounds`는 여전히 뷰의 내부 크기를 정확하게 나타냅니다.

![image](https://github.com/MojitoBar/iOS-DeepDive/assets/16567811/29b6a511-1d8f-49b5-98ca-2e9678ca38e3)
> 위 사진과 같이 뷰가가 회전한 경우 `frame`의 크기와 `bounds`의 크기가 다름을 알 수 있다.
