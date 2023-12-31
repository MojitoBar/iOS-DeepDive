# swift3 에서 c스타일 for문이 deprecated가 되었는데 왜 없어졌을까요?

swift3 버전 이전에는 c스타일의 for 문 `for(var i = 0; i < 10; i++)` 을 지원 했는데, swift3 버전이 되면서 없어졌다.

해당 내용은 [swift-evolution](https://github.com/apple/swift-evolution/blob/main/proposals/0007-remove-c-style-for-loops.md#remove-c-style-for-loops-with-conditions-and-incrementers) 레포에서 쉽게 찾을 수 있었다.

이유에 대해 나열하기 전에 스위프트 언어가 지향하는 발전 방향을 정리해봤다.

1. **안전성 (Safety)**: Swift는 안전한 프로그래밍을 지향함. 이는 옵셔널, 값 타입, 오류 처리, 타입 안정성 등의 특징을 통해 구현됨.
2. **성능 (Performance)**: Swift는 C와 C++와 같은 저수준 언어들의 성능에 근접하거나 뛰어나기를 목표로 함. 이를 위해 Swift는 매우 효율적인 컴파일러 최적화를 활용.
3. **표현력 (Expressivity)**: Swift는 현대적인 문법과 강력한 표준 라이브러리를 통해 코드가 명료하고 간결하게 작성될 수 있도록 지원함.
4. **자연스러운 문법 (Clarity)**: Swift는 코드의 명료성과 가독성을 중요하게 생각함. 이는 "오류를 최소화하면서 코드가 어떻게 동작하는지 명확하게 이해할 수 있어야 한다"는 철학에 기반함.
5. **소스 호환성 (Source Compatibility)**: Swift는 기존 버전과의 소스 코드 호환성을 중요하게 여기며, 큰 변경이 있을 때도 기존 코드의 작동을 깨트리지 않는 방향으로 노력하고 있음.
6. **커뮤니티 주도 (Community Driven)**: Swift는 오픈 소스 프로젝트로, 커뮤니티의 참여와 피드백을 중요하게 여김. Swift Evolution 프로세스를 통해 언어의 발전 방향을 커뮤니티와 함께 결정하고 있음.

이제 정확한 이유에 대해 정리해보자.

먼저, c스타일 for문에서 자주 사용되는 증감연산자가 먼저 제안된 것을 확인할 수 있었다.

[(증감 연산자-004, c스타일 for문-007)](https://github.com/apple/swift-evolution/tree/main/proposals)

증감연산자를 없애자는 제안이 이뤄진 이유는 증감연산자의 이점이 명확하지 않기 때문이었다.

1. x++는 x+=1 보다 코드가 짧지도 않고 훨씬 가독성이 좋은 것도 아니다.
2. 전위, 후위에 따라 작동하는 방식이 달라 실수하기 쉽고 혼란을 초래한다.
3. 자주 사용되지 않는 연산자이다.
4. swift 개발 초기에 별다른 고려없이 C에서 이월되었다. (레거시같은 의미인듯)

c스타일 for문이 논의된 배경도 이와 비슷하다.

1. 증감연산자가 없어진다면 해당 연산자가 가장 많이 사용되는 c스타일 for문을 사용하는 것이 어려워진다.
2. 이 역시 C언어의 잔재이며, 이를 대체할 for-in 구문이나 stride메소드가 존재한다.
3. for-in 구문이나 stride가 훨씬 스위프트에 어울린다. (코드가 명료하고 가독성이 좋다.)
4. 마찬가지로 Apple Swift 코드베이스 검사 결과 거의 사용되지 않는다.

결국 제안이 받아들여졌고 증감연산자와 C스타일 for문은 모두 Swift3 버전에서 사라지게 되었다.

토론 내용을 보면 증감 연산자와 c스타일 for문이 삭제된다면 기존에 작성되어있는 코드들을 어떻게 변환할 것인지 논의하는 부분이나 강하게 반대하는 의견도 종종 보여서 흥미로웠다.

그럼에도 크리티컬한 문제가 없다면 민심에 따라 반영되는 것을 보니 위에서 언급한 6번(커뮤니티 주도)가 굉장히 잘 지켜지는 것 같았다.

그리고 증감연산자 제거에 관한 proposal의 경우 Decision Note가 없었는데, 스위프트는 커뮤니티의 제안을 반영하기도 하고, 내부적으로 알아서 업데이트 하기도 하는 모양이다.
