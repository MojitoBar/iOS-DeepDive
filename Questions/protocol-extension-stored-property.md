# protocol, extension에서 stored property사용하는 방법

## protocol, extension에서의 stored property(저장 프로퍼티)

원래는 프로토콜과 익스텐션에서 저장프로퍼티를 아래의 이유 때문에 사용할 수 없다.

1. 프로토콜은 타입의 행위를 정의하는 추상화 도구이다. 이러한 프로토콜이 저장 프로퍼티를 가진다는 것은 프로토콜이 어떤 상태를 가져야 한다는 구체적인 구현 세부 사항을 강요하게 되므로 본래의 목적에 맞지 않다.
2. 익스텐션은 기존 타입에 새로운 기능을 추가하는 도구이다. 만약 저장 프로퍼티를 익스텐션에 추가할 수 있다면 이미 인스턴스화된 객체에 대해 어떻게 그 속성의 메모리가 할당되고 관리되는지에 대한 문제가 발생할 수 있다.
3. 이미 선언되어 있는 Int, String 등의 객체에도 저장 프로퍼티를 추가할 수 있게 되는 등 예측 불가능한 코드가 될 수 있다.

## associated object

AssociatedObject는 오브젝티브-C에서 제공하는 기능이다.

이를 사용하면 기존 클래스에 동적으로 속성을 추가할 수 있는데, 이 기능을 활용하여 프로토콜과 익스텐션에서 저장된 속성의 효과를 흉내낼 수 있다.

[objc*setAssociatedObject(*:_:_:\_:) | Apple Developer Documentation](https://developer.apple.com/documentation/objectivec/1418509-objc_setassociatedobject)

[objc_AssociationPolicy | Apple Developer Documentation](https://developer.apple.com/documentation/objectivec/objc_associationpolicy)

```swift
private var nameKey: UInt8 = 0

extension PropertyStoring {
    var name: String {
        get {
            return objc_getAssociatedObject(self, &nameKey) as? String ?? "Default Name"
        }
        set(newValue) {
            objc_setAssociatedObject(self, &nameKey, newValue, .OBJC_ASSOCIATION_RETAIN_NONATOMIC)
        }
    }
}

let myInstance = MyClass()
myInstance.name = "ChatGPT"
print(myInstance.name) // 출력: ChatGPT
```

Associated objects를 사용하면 저장 프로퍼티와 같은 동작을 흉내낼 수 있지만, 실질적으로는 저장 프로퍼티가 아니다.

내부적으로는 associated objects는 해당 객체와 연결된 별도의 key-value 저장소에서 값을 유지한다.

따라서 저장 프로퍼티와는 다르게, 객체의 메모리 레이아웃에 직접적으로 포함되지 않는다.

대신, Objective-C 런타임이 제공하는 별도의 메커니즘을 통해 객체와 연관된 값을 저장하고 검색하게된다.

## 왜 사용하는가?

위에서 언급한 이유로 저장 프로퍼티를 사용하는 것은 불가능 하지만 프로토콜이나 익스텐션에 저장 프로퍼티가 있으면 편한 경우가 있다.

블로그들을 찾아보니 실용적인 예시를 찾을 수 있었다.

1. UIScrollView에 마지막 y좌표를 저장할 프로퍼티를 만들어 스크롤 방향 확인하기
2. UIButton에 토클 상태를 저장할 프로퍼티를 추가하기
