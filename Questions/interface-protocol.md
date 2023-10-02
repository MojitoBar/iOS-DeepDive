# 자바 interface와 swift의 프로토콜의 차이점?

## 인터페이스는 파라미터의 기본 값을 지정할 수 있고, 프로토콜은 기본 값을 지정할 수 없다.

```swift
protocol TestProtocol {
    var number: Int = 100  // Error

    func getNumber() -> Int
    func setNumber(num: Int)
}
```

```java
public interface TestInterface {
    int number = 100;  // 상수로 간주됨.

    int getNumber();
    void setNumber(int num);
}
```

대신 프로토콜에서는 파라미터의 접근 유형을 지정해줄 수 있음 (getter, setter)

## 인터페이스는 모든 메소드를 구현해야하고, 프로토콜은 옵셔널을 통해 일부만 구현할 수 있다.

```java
class TestClass implements TestInterface {
    private int number;

    @Override
    public int getNumber() {
        return number;
    }

    @Override
    public void setNumber(int num) {
        this.number = num;
    }
}
```

```swift
@objc protocol MathProtocol {
    func add(a: Int, b: Int)

    @objc optional func subtract(a: Int, b: Int)
}

class MathClass: MathProtocol {
		// subtract 메서드 구현 안해도 됨.
    func add(a: Int, b: Int) {
        print(a + b)
    }
}
```

## 인터페이스에는 타입 메소드를 채택한 클래스에서 구현하지 못하지만 프로토콜에서는 타입 메소드를 구현할 수 있다.

```java
public interface MyInterface {
    static void myStaticMethod();  // 구현하지 않으면 오류남.
}

public interface MyInterface {
    static void myStaticMethod() {
        System.out.println("Static method in an interface.");
    }
}
```

```swift
protocol MyProtocol {
    static func typeMethod()
}

class MyClass: MyProtocol {
    class func typeMethod() {
        print("Type method in MyClass.")
    }
}
```
