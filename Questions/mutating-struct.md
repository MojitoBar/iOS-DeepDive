# struct에서는 왜 mutating키워드를 붙여줄까

swift의 `struct`는 값 타입이다. 값 타입의 중요한 특징 중 하나는 인스턴스의 속성이 기본적으로 **변경 불가능**하다는 것이다.

그러나 `mutating` 키워드를 사용하면 변경이 가능하다.

## mutating 키워드

`mutating` 키워드는 해당 메서도가 struct의 인스턴스 상태를 변경할 수 있다는 것을 명시적으로 나타낸다.

`mutating` 메서드가 호출될 때 일어나는 동작의 과정은 다음과 같다.

1. 메서드 호출 시, 현재 struct 인스턴스의 복사본이 생성된다.
2. 이 복사본 내에서 메서드의 코드가 실행된다.
3. 메서드 내에서 속성 변경이 일어나면, 이 변경은 복사된 인스턴스에 적용된다.
4. 메서드의 실행이 끝나면 원래 인스턴스는 이 복사본으로 교체된다.

```swift
struct Point {
    var x: Int
    var y: Int

    mutating func moveBy(x deltaX: Int, y deltaY: Int) {
        x += deltaX
        y += deltaY
    }
}

var point = Point(x: 0, y: 0)
point.moveBy(x: 5, y: 5)
print(point)  // Point(x: 5, y: 5)
```

위 예제에서 `moveBy(x:y:)` 메서드는 `mutating`으로 선언되었으므로 `point` 인스턴스의 `x`와 `y` 속성을 수정할 수 있다.

즉, `mutating` 키워드는 값 타입의 안정성을 유지하면서도, 필요한 경우 내부 상태를 변경할 수 있도록하는 키워드이다.
