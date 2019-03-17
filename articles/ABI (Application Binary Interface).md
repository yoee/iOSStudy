# ABI (Application Binary Interface)



Swift 공부를 하던 중, Swift에서 ABI의 안정성을 위하여 노력하고 있다는 글을 보았다. ABI가 뭐길래 그러는 것일까?

Wiki에서 딱히 와닿지 않은 설명을 읽다가, [Stackoverflow](https://stackoverflow.com/questions/2171177/what-is-an-application-binary-interface-abi)의 답변에서ABI에 관해 친절히 설명 해놓은 글을 읽었다.



## ABI란 무엇일까?

API는 익숙한 개념이겠지만, 다시 한 번 집고 나가보자. API는 우리가 써내려가는 code에 라이브러리나 OS에 있는 있는 data type/structures, constants, functions 등의 기능을 접근 및 사용할 수 있게 하는 것이다.

ABI 또한 이와 유사한 개념이다. 컴파일된 API 버전을 생각해보다. 우리가 소스코드를 작성할 떄, 우리는 API를 통하여 라이브러리에 접근한다. 마찬가지로, 만약 코드가 컴파일되게 되면, 우리의 어플리케이션은 ABI를 통하여 라이브러리 내의 바이너리 데이터에 접근할 수 있다. 그렇게 ABI는 우리의 컴파일된 어플리케이션이 external library에 접근하기 위해 사용할 structures와 methods를 정의할 수 있다.



## 참고

[참고](https://stackoverflow.com/questions/2171177/what-is-an-application-binary-interface-abi)

