# Swift 5.0

// 더 알려주고 싶은 것, 잘못 설명한 부분이 있다면 꼭!!! 알려주시기 바랍니다~~🤗🙏



---------------

## The Big Picture

Swift의 가장 큰 우선 순위는 **compatibility** 라고 합니다. 그리고, 이 compatibility는 두가지 목표를 가지고 있습니다.

- **Source compatibility**
- **Binary framework & runtime compatibility**



### Source compatibility

상위 버전의 컴파일러가 하위 버전의 Swift 코드를 컴파일 할 수 있다는 것 입니다. 우리에게 조금 와닿게 얘기하자면, 얘는 개발자가 새 Swift 버전이 나왔을 때, 해당 버전으로 migration하지 않아도 된다는 엄청난👍 장점을 가지고 있습니다.

이를 통하여, version-lock이라는 현상도 해결할 수 있습니다. 즉, 모든 소스와 패키지가 동일한 버전의 Swift로 작성되어져야 하지 않아도 된다는 말입니다.



### Binary framework & runtime compatibility

**Binary framework**가 Swift의 여러 버전과 호환될 수 있다는 이야기 입니다. Binary framework는 아래 두 가지를 포함합니다.

- **Swift 모듈 파일** (Swift module file) 
  - framework API의 소스 레벨에서 소통(communicate)합니다. (communicates source-level information of the framework's API)
  - the compiler's representation of the public interfaces of a framework. 
  - 컴파일러가 클라이언트 코드 컴파일 할 때, 필수적인 동작인 타입 검사나 코드 생성(?? code generation)에  쓰여짐.
- **공유 라이브러리** (shared library)
  - 런타임시 컴파일된 것을 제공합니다. (which provides the compiled implementation that is loaded at runtime)

그래서, **binary framework compatibility는 두가지 목표**를 가지고 있습니다. (ABI는 이어지는 단락에서 자세히 설명합니당.)

- **Module format stability**

  - 간단히 말하자면, 앱 개발자와 프레임워크(라이브러리) 작성자가 같은 버전의 컴파일러를 쓰지 않아도, 호환이 가능하다는 것입니다.
  - mixing versions of Swift at compile time
  - 장점
    - 앱의 라이브러리들을 rebuild하지 않아도, 새로운 버전의 컴파일러를 테스트 할 수 있습니다. 
    - 개발자는 그 모듈이 어떤 버전의 컴파일러로 빌드 되어 있는 지 신경 안써도 됩니다.

- **ABI stability**

  - mixing versions of Swift at run time

  

-------------

## ABI Stability

### ABI?

저는 잘 와닿지 않는 개념이었는데요. 먼저, 익숙한 개념인 API와의 비교를 통해서 알아보겠습니다. 

- API (Application <u>Programming</u> Interface)
  - 응용 프로그램에서 사용할 수 있도록, 운영 체제나 프로그래밍 언어가 제공하는 기능을 제어할 수 있게 만든 인터페이스를 뜻합니다.
- **ABI** (Application <u>Binary</u> Interface)
  - 응용 프로그램(의 바이너리)에서 사용할 수 있도록, 프레임워크나 라이브러리 내의 바이너리 데이터에 접근할 수 있도록 만든 인터페이스 입니다.

즉, <u>ABI는 API보다 오롯이 더 낮은(바이너리) 레벨에서 같은 역할</u>을 하는 친구 입니다.  그러니까, 아래와 같은 **low level detail들을 정의**할 수 있습니다.

- 어떻게 메모리에서 데이터를 나타낼 것인가 등… (CPU 명령어)
- 어떻게 함수를 호출할 것인가 등.. (Calling convention)
- metadata는 어디에 있으며, 얘한테는 어떻게 접근할 것인가… 



### ABI Stability

이제 ABI 안정성을 이해할 수 있을 것 같습니다. ABI는 컴파일된 앱이 외부 라이브러리의 바이너리 데이터와 통신 가능하게 했었습니다. 즉, ABI 안정성은 서로 다른 버전으로 컴파일된 바이너리 코드간의 통신이 가능하다는 것입니다! Swift로 예를 들면, ABI Stability를 지원한다는 말은, <u>컴파일된 앱이 다양한 버전의 Swift 바이너리 데이터를 접근/제어할 수 있게 된다는 말</u>이겠지요. 

좀 더 자세한 예시를 들면, Swift 3.0으로 컴파일된 앱을 Swift 4.0 라이브러리와 연결한다고 한다면, 당연히 실패해야겠지만, … Swift 5.0 부터는 Swift 6.0, 7.0 … 등과 잘 동작될 수 있다는 것입니다. 

#### 변화

그렇다면, ABI 안정성이 있을 때와 없을 때, 우리의 iOS 앱은 어떤 변화를 겪게 될까요? 

ABI Stability를 지원하지 않았던 기존 iOS 앱은, 같은 버전으로 작성된 Swift 코드와 Swift Dynamic Library/ABI를 가지고 있었습니다. (참고로 Swift Dynamic Library는 런타임시 로드되는 라이브러리 입니다. 얘는 .ipa안의 .dylib 형식으로 존재한다고 하는데, 약 5mb라고 하는군요!) 이 말은… 앱 마다 자신이 작성된 코드의 Swift 라이브러리를 가지고 있었다는 이야기 입니다.

그러나, ABI Stability를 지원하게될 iOS 앱은, OS 자체(iOS)가 Swift 라이브러리를 가지고 있게 됨으로서, 앱마다 Swift 라이브러리를 지니지 않아도 되게 되었다는 것이지요. 

#### 장점

- 앱 번들 사이즈가 줄어들 수 있습니다. (.dylib ㅃㅃ)
- 언어의 변화가 덜 자주, 더 적게 일어날 것입니다.
- migration을 덜 해도 될 것입니다.
- Swift를 지니고 있을 필요가 없으니, 미리 컴파일된 프레임워크를 만들 수 있을 것입니다. (현재 프레임워크는 앱을 컴파일할 때 같이 컴파일 됩니다) 

#### 단점

- Limits changes to the Public Interfaces and Symbols. // 2번째에 쓴 장점과 연결되네요
- Restricts the ways Swift can grow and evolve



-------------------

## 참고

- [Swift] [Swift 5.0 Release Process](https://swift.org/blog/5-0-release-process/) 
- [Swift] [Plan for module stability](https://forums.swift.org/t/plan-for-module-stability/14551) : module stability가 가능한 방법에 관해서도 나와 있는데, 여기서는 안다뤘어요.
- [Swift] [Swift ABI Stability Manifesto](https://github.com/apple/swift/blob/master/docs/ABIStabilityManifesto.md)
- [stackoverflow] [What is an application binary interface (ABI)?](https://stackoverflow.com/questions/2171177/what-is-an-application-binary-interface-abi) 
- [blog] [ABI stability](https://zeddios.tistory.com/654) : 한글 설명 
- [blog] [What will be new in Swift 5?](https://developerinsider.co/what-will-be-new-in-swift-5/)
- P.S [blog] [What’s new in Swift 5.0](https://www.hackingwithswift.com/articles/126/whats-new-in-swift-5-0) 