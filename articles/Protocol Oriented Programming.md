# Protocol 잘 사용해보기

for 3/18 meeting of Cleanios, by yoee



[TOC]



-------------

## Intro

재사용성과 모듈화를 돕는 데에, 강력한 역할을 하는 Protocol의 강점에 관하여 간단히 정리하고, 그것을 "유려하게" 활용하는 방법에 관하여 공부해봅시당!

> [유려하다] : 글이나 말, 곡선 따위가 거침없이 미끈하고 아름답다.

// 첫 스터디 시간의 발표인 만큼, iOS 개발의 기본이 되어지는 Protocol에 관하여 집고 넘어가보고 싶어 준비해보았습니다. 

- 강점이 무엇인지 정확히 알자
-  적용하는 기법들에는 어떤 것들이 있는 지 알자
- 그 예시는 어떠한 지 -> 내가 "유려하게" 사용할 수 있도록 숙지하자!
- 잘못 사용하는 예시는 무엇일까 ? - 사용할 때 자주 하는 실수는 무엇인지… 객체 지향적인 개발에서 주요하게 생각되어지는 SOLID(잘은 모르지만ㅎㅎ 형중님 의견 두근…)를 지키는 방향으로…



-----------------

## Swift를 좋아하는 이유 중의 하나, Protocol

### Protocol의 장점



### 참고

[10 things I like about Swift](https://medium.com/ios-os-x-development/10-things-i-like-about-swift-7bbd40cabb79)



-----------

## How Protocol Oriented Programming in Swift saved my day?

### OOP로는 부족한가요?

- 불필요한 복잡성

  이러한 강점들을 주지만… encapsulation,  access control, abstractions… 그런데, 하나의 class에서 시작하여, 그 기능을 필요로 하는 애들이 상속을 계속 계속 받게 되는 구조는, 불필요한 복잡성을 줄 수 있습니다.

- 멀티 스레드 환경에서 참조형으로 인한 충돌/예상치 못한 행동
- ? 결합도가 높아져, 하나의 클래스를 위한 Unit test를 작성하기 어렵다.



### 일등 시민, Structs and Enum

> Swift from the very beginning has embraced the idea of value types. Structs and Enums are first class citizens in Swift and come packed with a lot of features like properties, methods and extensions which are only find in Classes in most languages. Although value types do not support inheritance in Swift, they can conform to protocols which allows them to enjoy the benefits of Protocol Oriented Programming.





### 참고

[How Protocol Oriented Programming in Swift saved my day?](https://medium.com/ios-os-x-development/how-protocol-oriented-programming-in-swift-saved-my-day-75737a6af022)

------------

## 단점은 없나용?







--------------

## typealias, compostion과 함께 사용하기





----------

## 접근 제어자와 함께 사용하기



















