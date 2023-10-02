# static만 있을경우 왜 struct나 class대신에 enum을 써야하는가?

가장 중요한 이유는 “인스턴스화를 할 수 없다”인 것 같다.

객체에 `static`만 있다는 것은 타입 프로퍼티와 타입 메소드만 존재한다는 뜻이다.

즉, 인스턴스를 할 필요가 없고, 해도 사용할 기능이 없다는 뜻이다.

이 경우에 `struct`나 `class`가 아니라 `enum`을 사용하여 구현하게 되면 실수로라도 인스턴스로 선언하는 것을 방지할 수 있다. 그리고 코드를 읽을 때 인스턴스화 할 수 없다는 의도를 명확하게 할 수 있다.

또한 enum은 struct나 class에 비해 더 경량화된 구조를 가진다. 즉 메모리나 초기화에 관련한 오버헤드가 없다.

```swift
enum Utility {
    static let someValue = "Value"
    static func doSomething() {}
}

let instance = Utility()  // 컴파일 에러
```
