# 옵셔널 타입 클로저 매개변수는 왜 escaping이 기본인가?

`@escaping` 키워드는 Swift3부터 추가된 키워드이다.

이전에는 클로저가 escaping이 기본값이었으며, `@noescape` 키워드를 이용해 non-escaping 클로저를 선언할 수 있었다.

하지만 아래와 같은 이유로 Swift3부터는 non-escaping을 기본으로하고, `@escaping` 키워드를 붙이는 식으로 변경되었다.

[non-escaping 깃허브 proposal 링크](https://github.com/apple/swift-evolution/blob/main/proposals/0103-make-noescape-default.md)

1. **기능적 알고리즘의 이점**: 순수 스위프트로 작성된 대부분의 함수형 알고리즘은 자연스럽게 non-escaping입니다. 이로 인해 이러한 알고리즘을 작성할 때 필요한 보일러플레이트 코드가 줄어듭니다.
2. **컴파일러의 질의 향상**: 개발자가 클로저의 escaping에 대해 신경 쓰지 않고 클로저를 escaping 시도할 때, 컴파일러는 이를 감지하고 **`@escaping`** 을 추가하는 것을 제안하는 fixit을 제공할 수 있습니다.
3. **언어의 선호도 변경**: 최근의 변경사항(예: inout 매개변수에 대한 escaping 클로저의 사용 금지)은 언어가 non-escaping 클로저를 선호하도록 밀어주고 있습니다. 또한, non-escaping 클로저는 참조 순환 문제의 한 분류를 제거함으로써 항상 선호되어 왔습니다.
4. **@autoclosure(escaping)의 표준화**: "@autoclosure(escaping)"은 "@autoclosure @escaping”으로 더 간단하고 표준화된 형식으로 변환될 수 있습니다.

> 그런데, 클로저 매개변수를 옵셔널 타입으로 받게되면 클로저는 escaping이 기본값이 된다. 왜 일까?

이유는 옵셔널로 한번 감쌌기 때문이었다.

[[SR-2444] @escaping failing on optional blocks · Issue #45049 · apple/swift](https://github.com/apple/swift/issues/45049#comment-17861)

클로저의 기본값이 non-escaping이 되는 경우는 **“클로저 타입이 매개변수로 전달될 때”**이다.

하지만 옵셔널 타입 클로저 매개변수는 말 그대로 클로저 타입이 아니라 옵셔널 타입이기 때문에 위 법칙이 적용되지 않는다. 따라서 escaping이 기본으로 동작하게 되는 것이다.
