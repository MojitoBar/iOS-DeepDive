# 접근제어자

1. **private**:

   - 선언이 위치한 코드 블럭 내에서만 접근 가능.
   - 예를 들어, 클래스 내의 특정 메서드나 프로퍼티에 **`private`**을 사용하면, 해당 클래스의 다른 메서드에서는 접근이 가능하지만, 동일 파일의 다른 클래스나 구조체에서는 접근할 수 없음.
   - Swift4부터는 같은 파일 내의 extension에서는 접근이 가능해짐.

   ```swift
   struct Square {
       private var sideLength: Double

       init(sideLength: Double) {
           self.sideLength = sideLength
       }
   }

   extension Square {
       func area() -> Double {
           return sideLength * sideLength  // Swift 4부터 `private` 프로퍼티에 접근 가능
       }
   }

   let square = Square(sideLength: 5)
   print(square.area())  // 출력: 25.0
   ```

2. **fileprivate**:
   - 현재 소스 파일 내 어디에서나 접근 가능합니다.
   - **`private`**보다 넓은 범위를 가지며, 같은 소스 파일 내의 다른 타입들과의 상호작용에 필요할 때 사용됩니다.
3. **internal**:
   - 기본 접근 수준입니다. 명시하지 않으면 **`internal`**로 간주됩니다.
   - 해당 모듈(Module) 내에서는 어디에서나 접근 가능하나, 모듈 외부에서는 접근할 수 없습니다.
4. **public**:
   - 해당 모듈 외부에서도 접근 가능합니다.
   - 일반적으로 라이브러리나 프레임워크의 공개 API의 일부로 사용됩니다.
5. **open**:
   - **`public`**과 비슷하게 해당 모듈 외부에서도 접근 가능합니다.
   - 차이점은, **`open`**으로 선언된 클래스는 다른 모듈에서 상속받을 수 있습니다. 또한, **`open`**으로 선언된 클래스 메서드는 오버라이드할 수 있습니다.

## class, static func의 차이

둘 다 타입 메소드로 사용되지만 차이점이 있다.

1. **static func**
   - **`static`**으로 선언된 메서드는 오버라이드 될 수 없다.
   - 해당 메서드가 선언된 타입 자체에 연결되어 있기 때문에 서브클래스에서 재정의할 수 없다.
2. **class func**
   - **`class`**로 선언된 메서드는 오버라이드 될 수 있다.
   - 오직 클래스에서만 사용될 수 있다. 구조체나 열거형에서는 **`class func`**을 사용할 수 없다.
   - 서브클래스에서 해당 메서드의 기능을 재정의하거나 확장하려는 경우에 유용하다.

```swift
class Animal {
    class func sound() {
        print("Some sound")
    }
}

class Dog: Animal {
    override class func sound() {
        print("Woof!")
    }
}

Animal.sound() // 출력: Some sound
Dog.sound()    // 출력: Woof!
```

만약 static으로 선언했다면 오버라이드 할 수 없었을 것이다.
