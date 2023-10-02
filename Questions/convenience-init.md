# convenience init이 무엇인가? 일반적인 init과의 차이점이 무엇인가?

Swift에서 `convenience` 초기화 메서드는 특정 클래스에 대한 보조 초기화 메서드를 제공하는 데 사용된다.

`convenience` 초기화 메서드는 항상 같은 클래스 내의 다른 초기화 메서드를 호출해야 함.

이로 인해 다양한 초기화 방법이나 기본 값을 제공하는데 유용합니다.

1. Delegating Initializer:
   - `convenience init`은 다른 초기화 메서드를 호출해야 한다.
   - 이는 클래스의 주 초기화 메서드를 통해 항상 모든 프로퍼티가 올바르게 초기화됨을 보장하기 위함.
2. Intended Use:
   - 일반적인 `init`은 클래스의 모든 프로퍼티를 직접 초기화하는 "주(initial)" 초기화 메서드의 역할을 한다.
   - `convenience init`은 보조 초기화 메서드로, 일반적으로 주 초기화 메서드에 대한 간편한 또는 변형된 버전을 제공하는 데 사용한다.

> 보조 초기화 (convenience init)이 필요한 이유

복잡한 객체를 생성하는 데 필요한 다양한 매개변수를 가진 주 초기화가 있을 때, 일부 값만 변경하거나 기본 값을 설정하는 등의 새로운 초기화가 필요할 때 기존의 초기화 코드를 똑같이 작성하는 것은 불필요하고 비효율적이다.

따라서 보조 초기화를 활용하여 더 적은 코드로 쉽게 객체를 생성할 수 있다.

아래는 간단한 예시:

```swift
class Pizza {
    var size: Int
    var toppings: [String]

    // 주 초기화 메서드
    init(size: Int, toppings: [String]) {
        self.size = size
        self.toppings = toppings
    }

    // 보조 초기화 메서드
    convenience init() {
        self.init(size: 12, toppings: ["Cheese"])
    }
}

let cheesePizza = Pizza()  // size = 12, toppings = ["Cheese"]
let customPizza = Pizza(size: 16, toppings: ["Pepperoni", "Mushrooms"])
```
