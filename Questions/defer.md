# defer가 어떨때 동작안할까?

`defer` 는 코드 블럭을 나가기 전에 실행되게 하는 키워드이다.

컴파일러는 `defer` 블록 내의 코드를 적절한 위치, 즉 함수가 반환되기 직전의 위치로 이동시키는 방식으로 동작한다고 한다.

```swift
func example() {
    defer { print("World!!") }
    print("Hello")
}
```

예를들어 위와 같은 코드를 실행하면 “World!!”보다 “Hello”가 먼저 찍히게 된다.

defer는 후입선출 로직으로 동작하는데,

```swift
func example() {
    defer { print("1") }
    defer { print("2") }
    defer { print("3") }
    defer { print("4") }
    defer { print("5") }
    defer { print("6") }
}
```

위 코드는 먼저 작성된 1이 가장 나중에 출력되어 6 → 5 → 4 → 3 → 2 → 1 순으로 찍히게 된다.

이는 함수의 호출과 리턴 매커니즘이 스택으로 동작해서 똑같이 스택으로 동작하는 것 같다.

아무튼 이런 특성을 가진 **defer 구문이 동작하지 않는 경우**가 있다.

바로 컴파일러가 defer 구문을 읽기 전에 함수가 종료되어 버리는 경우이다.

```swift
func example() {
    var a = 0

    if a == 0 {
        return
    }

    defer {
        print("test")
    }
}
```

위 예제가 그런 경우이다.

이러한 경우엔 컴파일러가 defer 구문을 읽기전에 함수가 종료되므로 defer 구문이 동작하지 않는다.
