# UIScene, UIWindowScene, UIWindow

코드 베이스로 작업하려고 아래 코드를 작성하다 궁금해서 공부한 내용.

```swift
func scene(_ scene: UIScene, willConnectTo session: UISceneSession, options connectionOptions: UIScene.ConnectionOptions) {
    // Use this method to optionally configure and attach the UIWindow `window` to the provided UIWindowScene `scene`.
    // If using a storyboard, the `window` property will automatically be initialized and attached to the scene.
    // This delegate does not imply the connecting scene or session are new (see `application:configurationForConnectingSceneSession` instead).

    guard let windowScene = (scene as? UIWindowScene) else { return }

    let window = UIWindow(windowScene: windowScene)
    window.rootViewController = ViewController()
    window.makeKeyAndVisible()

    self.window = window
}
```

1. **UIScene**:
   - 이것은 앱의 사용자 인터페이스의 한 인스턴스나 "상태"를 추상적으로 나타내는 기본 클래스입니다.
   - 앱의 UI와 그에 관련된 이벤트 및 생명 주기를 관리합니다.
2. **UIWindowScene**:
   - **`UIWindowScene`**은 **`UIScene`**의 구체적인 하위 클래스입니다.
   - 특히 앱의 그래픽 사용자 인터페이스와 관련된 씬을 나타냅니다.
   - 화면의 물리적 특성, 해상도, 화면 크기 등과 관련된 설정 및 정보를 제공합니다.
   - 하나의 **`UIWindowScene`**은 하나 이상의 **`UIWindow`** 객체를 관리할 수 있습니다.
3. **UIWindow**:
   - **`UIWindow`**는 **`UIWindowScene`**에 연결된 실제 그래픽 객체입니다.
   - 앱의 뷰 계층을 호스팅하며 화면에 직접적으로 그려지는 유일한 객체입니다.
   - **`UIWindow`**는 특정 **`UIWindowScene`**에 연결되어야 하며, 이 연결을 통해 화면에 렌더링됩니다.

iOS 13 이전에는 Window에서 앱의 상태까지 같이 관리했는데, 13 이후에 아이패드에서 멀티 태스킹을 지원하게 되면서 앱의 상태를 관리하는 클래스(UIScene)을 따로 분리함. 왜냐하면 하나의 앱에서 여러개의 앱 상태를 지원해야하기 했기 때문에.

그래서 AppDelegate만 있었던 것이 AppDelegate와 SceneDelegate로 나뉘게 되었음.

그리고 iOS 13 이후부터는 SceneDelegate에서 앱의 상태를 관리하기 때문에 만약 앱 시작 윈도우를 커스텀하게 설정하고 싶다면(스토리보드 말고 코드 베이스로) 이 파일에서 작업해야한다.

> 그럼 UIWindowScene은 뭘까?

UIWindowScene은 UIScene의 서브클래스로, 앱의 추가적인 상태가 담겨있는 클래스이다.

예를 들어 화면 크기나 가로/세로 모드, 다크모드 상태 등등.

그래서 window를 만들기 위해선 UIScene 객체를 UIWindowScene으로 타입 캐스팅 해주어야 한다.

그리고 rootViewController로 설정한다고 끝나는게 아니라 makeKeyAndVisible()를 꼭 호출해주어야한다.

이 함수는 해당 윈도우를 keyWindow로 설정하겠다는 뜻인데, 키 윈도우는 사용자의 상호작용(터치, 키보드)을 받아들이는 윈도우를 뜻한다.

만약에 기본으로 제공되는 Main 스토리보드를 사용한다면 자동으로 UIWindow가 생성되고 키 윈도우를 설정한다.

하지만 나는 코드베이스로 커스텀하게 window를 만들어줬기 때문에 이 함수를 꼭 호출해야한다.

---

```swift
var window: UIWindow?

func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    // Override point for customization after application launch.
    if #available(iOS 13.0, *) {
        return true
    }

    window = UIWindow()
    window?.rootViewController = ViewController()
    window?.makeKeyAndVisible()

    return true
}
```

AppDelegate에서는 13버전 이전만 대응하면 되는데 13버전 이전에는 Scene이 없기 때문에 바로 window를 생성해서 rootViewController를 세팅해주면 된다.
