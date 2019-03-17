# Swift 5.0 에서 바뀌는 것

마음에 와닿은 몇 몇 가지만 가져와보았습니다.



## ABI Stability

먼저, 



## [SE-0192](https://github.com/apple/swift-evolution/blob/master/proposals/0192-non-exhaustive-enums.md)  Handling Future Enum Cases

``` Swift
enum Cake: CaseIterable {
    case chocolate
    case carrot
}

// example
switch cake {
case .chocolate:
    break
default:
    break
}
```

아주 평범한 enum과, 그에 관한 사용 예시입니다.

기존의 enum에서 처리가 필요한 케이스는 처리를 하고 -> 그럴 필요가 없는 아이는 default 처리를 넣어주었는 경우이지요.

그런데, 이 때, 새로운 케이스가 추가 되었다고 생각해봅시다. 그리고… 우리는 이후 이 소스를 실행하여도, (컴파일 딴에서는) 아주 평화로울 것이라는 예상을 할 수 있습니다. 케이스를 사용하던 곳에서는 별다른 에러를 내지 않고 default에서 처리해준 내용을 사용하게 될 것입니다.

??? 이건 과연 좋은 것일까요

우리는 새로운 케이스에 관한 대응을 미처 하지 못하고, 예상치못한 default 속의 기능을 쓰게 될 지도 모릅니다..ㅠㅠ 이러한 경우를 잡아주기 위하여 스위프트는 `@unknown`이라는 annotation(?)을 추가해주었습니다. 

```Swift
enum Cake: CaseIterable {
    case chocolate
    case carrot
    case cheese // new case!
}

// example
switch cake { // WARNING : Switch must be exhaustive
case .chocolate:
    break
@unknown default:
    break
}
```

 `@unknown`을 추가해줌으로서, 워닝이 생겼고, 우리는 처리하지 않은 케이스들에 관하여 상기할 수 있습니다. 