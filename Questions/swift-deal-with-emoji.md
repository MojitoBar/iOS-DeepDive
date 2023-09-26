# 가족 이모지 같은경우 swift에서는 4개의 이모지를 조합해서 사용하다보니 서버에 전달했을경우 오류가 발생하는 경우가 있습니다. 어떻게 하면 좋을까요?

```swift
let familyEmoji = "👨‍👩‍👧‍👦"
print(familyEmoji.count)  // 1
print(familyEmoji.unicodeScalars.count)  // 여러 개의 코드 포인트를 반환
```

위 코드를 실행해보면 텍스트의 길이는 1이지만 [유니코드 스칼라](https://developer.apple.com/documentation/swift/unicode/scalar)는 7이 찍히는 것을 볼 수 있다.

이는 특정 이모티콘의 경우 이모지 + ZWJ(이모지 조합자)의 합으로 이뤄지기 때문이다. 따라서 모든 문자를 안전하게 표현할 수 있는 형태로 서버에 전달해야한다.

예를들어 ASCII나 ISO-8859이런 인코딩의 경우엔 이모지를 지원하지 않는다.

옛날 인코딩의 경우 이모지 이외에도 국제 문자를 표현하는데에 한계가 명확한데, 여러 국가와 언어를 하나의 통일된 문자 집합으로 표현하기 위해 만들어진 것이 [유니코드](https://en.wikipedia.org/wiki/Unicode)이다.

그리고 유니코드 문자를 인코딩하는 방법은 uft-8, uft-16 등이 있다.

가족 이모티콘의 경우 다음과 같은 7개의 유니코드 코드 포인트로 이루어져 있다.

1. 👨 (U+1F468) - Man
2. ‍ (U+200D) - Zero Width Joiner (ZWJ)
3. 👩 (U+1F469) - Woman
4. ‍ (U+200D) - Zero Width Joiner (ZWJ)
5. 👧 (U+1F467) - Girl
6. ‍ (U+200D) - Zero Width Joiner (ZWJ)
7. 👦 (U+1F466) - Boy

```swift
let emoji = "👨‍👩‍👧‍👦"
let buf: [UInt8] = Array(emoji.utf8)

print(buf)
// [240, 159, 145, 168, 226, 128, 141, 240, 159, 145, 169, 226, 128, 141, 240, 159, 145, 167, 226, 128, 141, 240, 159, 145, 166]
```

이 코드를 실행해보면 25개의 바이트로 이뤄져있고 값을 보면,

[226, 128, 141]가 4바이트 마다 등장하는 것을 볼 수 있는데 이 코드가 ZWJ인 것 같다.

그러니까 이모티콘 4 _ 4 + ZWJ 3 _ 3 해서 25개로 나오는 듯 하다.

아무튼 서버에 전달했는데 문제가 발생했다면 유니코드를 지원하는 인코딩을 사용했는지 먼저 확인해야한다. 그리고 서버측에서도 동일한 포멧(utf-8)을 사용하는지 확인해야한다. (데이터베이스 테이블 컬럼 등)

왜나하면 모두 유니코드를 지원하는 인코딩이라해도 서로 다른 바이트 구조를 사용하기 때문이다.

모두가 유니코드를 지원하는 동일한 인코딩을 사용하고 있다면 어떤 이모지나 국제문자를 보내도 문제가 없을 것이다.

### 추가로 찾아본 내용

### **UTF-8:**

**장점**:

1. **ASCII 호환성**: 기존의 ASCII 문자(0-127)는 UTF-8에서도 1바이트로 표현됩니다. 이로 인해 많은 기존 시스템과 소프트웨어가 UTF-8을 쉽게 채택할 수 있었습니다.
2. **변동 길이 인코딩**: 1바이트에서 4바이트까지 문자에 따라 다양한 길이의 바이트를 사용합니다. 이로 인해 영어나 숫자와 같은 문자는 효율적으로 저장됩니다.
3. **웹 표준**: UTF-8은 웹에서 가장 널리 사용되는 인코딩 방식입니다.

**단점**:

1. **길이 변동**: 문자에 따라 바이트 길이가 다르므로, 특정 위치의 문자를 알기 위해서는 문자열을 처음부터 탐색해야 할 수 있습니다.
2. **메모리 사용**: 아시아 언어와 같이 비ASCII 문자를 주로 사용하는 문자열의 경우, UTF-8은 UTF-16보다 더 많은 바이트를 사용할 수 있습니다.

### **UTF-16:**

**장점**:

1. **2바이트 기본 단위**: 많은 유니코드 문자가 2바이트로 표현됩니다. 이는 아시아 문자 등 많은 문자들에 대해 상대적으로 효율적입니다.
2. **일부 시스템 통합**: Windows와 Java 같은 시스템과 플랫폼에서 내부적으로 사용되므로, 이 환경에서는 자연스럽게 적합합니다.

**단점**:

1. **비ASCII 문자의 추가 비용**: ASCII 문자는 UTF-8에서 1바이트로 표현되지만, UTF-16에서는 2바이트가 필요합니다.
2. **서로게이트 쌍**: 유니코드의 범위를 넘어서는 문자를 표현하기 위해서는 4바이트를 사용해야 합니다. 이로 인해 인코딩과 디코딩이 복잡해질 수 있습니다.
3. **인코딩(Encoding)**
   - **정의**: 원래의 데이터나 정보를 특정 포맷이나 표준으로 변환하는 과정입니다.
   - **목적**: 데이터를 안전하게 전송하거나 저장하기 위해서, 특정 목적에 맞게 데이터를 변환하거나 압축하기 위해 인코딩을 사용합니다.
   - **예시**: 텍스트 문자열을 UTF-8로 인코딩하여 바이트 시퀀스로 변환하는 것.
4. **디코딩(Decoding)**
   - **정의**: 인코딩된 데이터나 정보를 원래의 형식으로 복원하는 과정입니다.
   - **목적**: 전송되거나 저장된 인코딩된 데이터를 읽거나 사용하기 위해 원래의 형태로 복원합니다.
   - **예시**: 바이트 시퀀스를 UTF-8 디코딩하여 원래의 텍스트 문자열로 복원하는 것.

---

궁금했던 점은 이모지가 생각보다 자주 업데이트 되는 것 같던데 전부 유니코드에 등록이 되는건가?

찾아보니 애초에 제안을 먼저 하는거 같았다. 새로 추가할 이모지를 Unicode Consortium에 제안하고 검토 과정을 거쳐서 채택된다고 한다.

그러다 이모지가 너무 많아지면 어떻게 되지?도 궁금했다.

유니코드는 문자에 고유한 번호, 즉 "코드 포인트"를 할당하기 위한 시스템이다. 유니코드 표준은 다양한 평면(Plane)으로 구성되며, 현재 총 17개의 평면이 있다고 한다.

각 평면은 65,536(= 2^16)개의 코드 포인트를 포함하고 있기 때문에 전체 유니코드 코드 포인트의 수는 17 × 65,536 = 1,114,112개이다.

이 중 현재 할당되어 있는 문자는 약 14만개 정도라고 하니 걱정할 필요는 없는 것 같았다.