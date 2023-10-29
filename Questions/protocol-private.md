# protocol에선 왜 private를 못쓸까?

스위프트에서 프로토콜은 타입의 행위를 정의하는 역할을 한다.

이는 해당 프로토콜을 채택한 타입이 준수해야 하는 요구사항을 나열하는 것인데, 프로토콜 내에서 `private` 은 본래의 역할과 상반된다.

`private`을 사용하면 해당 요구 사항이 프로토콜을 정의하는 스코프 외부에서는 보이지 않게 되므로, 이를 채택한 타입에서 해당 요구 사항을 실제로 구현할 수 없게 된다.

즉, 프로토콜의 요구 사항은 그것을 채택한 타입에 의해 반드시 볼 수 있고 구현될 수 있어야 한다.

그런데 `protocol`에서는 `private` 뿐만 아니라 모든 접근 제어자를 붙일 수 없다.

이유는 위에서 설명한 것과 비슷한데,

> 프로토콜의 요구 사항이 해당 프로토콜을 채택한 모든 타입에 대해 명시적이고 접근 가능해야 하기 때문이다.

만약 요구 사항에 접근 제어자를 붙이면, 그 요구 사항이 어떻게 접근되어야 하는지에 대해 혼란이 생길 수 있다.

따라서 프로토콜의 내부 요구 사항들은 프로토콜의 접근제어자를 따른다.