# weak, unowned의 차이점은 무엇일까?

## 성능차이가 왜 발생할까?

[](https://github.com/apple/swift/blob/main/stdlib/public/SwiftShims/swift/shims/RefCount.h)

1. **참조 카운트 (RefCounts)**:
   - 각 객체는 세 가지 참조 카운트를 가진다. strong, unowned, weak.
   - 이러한 카운트는 객체 내부에 직접 저장되거나 "side table entry"에 저장된다.
2. **참조 카운트의 동작**:
   - **Strong RC**: 객체에 대한 강한 참조를 계산한다. 이 카운트가 0이 되면 객체는 deinitialized되고, unowned 참조 읽기는 오류가 발생하며, weak 참조 읽기는 nil이 된다.
   - **Unowned RC**: 객체에 대한 unowned 참조를 계산한다. 이 카운트가 0이 되면 객체의 할당이 해제된다.
   - **Weak RC**: 객체에 대한 약한 참조를 계산한다. 이 카운트가 0이 되면 side table entry가 해제된다.

메모리가 실질적으로 해제되는 조건은 다음과 같다.

1. **DEINITING 상태**: **`deinit()`** 메소드가 호출되고 완료될 때 객체의 strong 참조 카운트가 0이고 unowned 참조가 없다면, 객체는 메모리에서 즉시 해제된다. 그렇지 않으면 DEINITED 상태로 전환됨.
2. **DEINITED 상태**: 객체의 **`deinit()`** 메소드가 이미 호출되었지만 여전히 unowned 참조가 남아 있는 상태. 이 상태에서 unowned 참조 카운트가 0이 되면 객체는 메모리에서 해제된다.
3. **FREED 상태**: 객체는 이미 메모리에서 해제되었지만, side table에 대한 약한 참조가 아직 있을 때의 상태. 이 상태에서 weak 참조 카운트가 0이 되면 side table 엔트리도 해제된다.

![Untitled](https://www.vadimbulavin.com/assets/images/posts/memory-management/heap-object-lifecycle.svg)

Dead 상태가 실질적으로 객체의 메모리가 해제된 상태이다.

위 깃허브 링크의 주석을 읽어보면 객체가 처음 초기화될 때 3개의 참조 카운터는 각각 1, 1, 1로 초기화 된다.

그리고 strong 참조 카운트가 0이되어 deinit이 호출되면 unowned 참조 카운트도 1 감소한다.

만약 unowned 참조 카운트가 0이 된다면 인스턴스가 메모리에서 해제되는 Freed 상태가 된다.

weak 참조 카운트는 객체가 메모리에서 해제되면 1 감소하는데, 참조 카운트가 0이되면 side table entry가 메모리에서 해제된다.

> 잘 이해했는지 모르겠는데, weak 참조 변수는 객체가 아니라 사이드 테이블을 참조하기 때문에 참조하는 객체가 nil이 될 때 한 번에 해제할 수 있는 것 같다.

결론은 weak의 경우 사이드 테이블이라는 별도의 메모리 구조를 사용하기 때문에 메모리 및 관련 연산 오버헤드가 더 많다. 따라서 unowned를 사용할 경우 성능 면에서 이점을 챙길 수 있다.

## 어떨때 사이클이 확실해서 unowned를 쓰면 좋을까?

unowned를 오류없이 사용하기 위해서는 두 객체 간의 참조 관계가 명확하게 정의되어 있어야 한다.

객체 내에서 클로저를 정의하고, 해당 클로저가 객체를 참조하는 경우가 그렇다.

```swift
class SomeClass {
    var value = 0

    lazy var increment: () -> () = { [unowned self] in
        self.value += 1
    }
}

let instance = SomeClass()
instance.increment()
print(instance.value) // 출력: 1
```

이 경우 클로저의 생명주기는 항상 클래스보다 짧음을 확신할 수 있다.

왜냐하면 클로저가 인스턴스를 벗어난 생명주기를 가지기 위해서는 escaping 키워드가 필수이기 때문이다.

따라서 weak말고 unowned를 사용하여 성능면에서 이점을 챙길 수 있다.

> 좀 더 실용적인 예시는 생각이 안난다..
