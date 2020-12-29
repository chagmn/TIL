# Unit Test 사용해보기

Unit Test는 한국어로 단위 테스트 또는 유닛 테스트라고 한다. Unit Test는 학부 때 소프트웨어 공학이라는 강의에서 배웠던 내용이다. 개발하는 과정 중 Unit Test가 가장 기초적이면서 중요하다고 생각이 난다. 그래서 Xcode에서 Unit Test를 하는 방법에 대해 이야기하려고 한다.

이 글은 아래 글을 참고해서 정리했습니다.
https://zeddios.tistory.com/48

---

## Unit Test?

Unit Test는 무엇일까? 바로 소스 코드에서 특정 모듈, 클래스가 개발자가 의도한 대로 정확하게 작동하는지 테스트하는 과정이다. 즉, 모든 함수나 메소드에 대한 테스트 케이스를 작성하는 과정이다.</br>

## 왜 Unit Test가 필요한가?

크게 Unit Test는 프로그램 내의 버그를 찾아내고 코드의 퀄리티를 높이기 위해 만든다. 만약, 개발한 프로그램이 크고 메모리가 많이 들어서 로컬 환경에서 실행시키기 어려운 경우 개발자들은 Unit Test를 만들어서 빠르게 본인의 코드가 제대로 작동하는지 확인할 수 있다.

## Xcode에서 Unit Test 사용

시작하기 앞서, 사용하는 Xcode 버전은 12.3 (12C33) 입니다.

![시작](https://user-images.githubusercontent.com/41609708/103275921-9088a480-4a08-11eb-9c8b-49a370b44b5c.jpg)

프로젝트를 생성할 때 다음과 같이 Include Tests에 체크를 해준다. 전 버전에서는 Test와 UITest 체크 부분이 각각 존재했지만 합쳐진 것으로 보인다.

![메뉴](https://user-images.githubusercontent.com/41609708/103275955-a5fdce80-4a08-11eb-8193-ed22a1703d9e.jpg)

그럼 다음과 같이 `프로젝트명Test`와 `프로젝트명UITest` 폴더가 생성 될 것이다. 그 중 Test폴더에 있는 Swift 파일을 보면 다음과 같다.

![코드](https://user-images.githubusercontent.com/41609708/103275956-a72efb80-4a08-11eb-9823-678e6175db64.jpg)

클래스를 보면 `XCTestCase`를 상속받고 있으며 `setUpWithError()`, `tearDownWithError()`, `testExample()`, `testPerformanceExample()` 함수들이 있다.

XCTestCase 클래스는 테스트 케이스,
테스트 메소드 등을 정의하기 위한 클래스다. 그리고 각각의 메소드는 다음과 같은 역할을 한다.

1. setUpWithError() :  
   초기화 코드를 작성하는 함수로 클래스의 각 테스트 함수의 호출 전에 호출되는 함수다.
2. tearDownWithError() :  
   해체 코드를 작성하는 함수로 각 테스트 함수의 호출 후에 호출되는 함수다.
3. testExample() :  
   테스트 케이스를 작성하는 함수로 테스트가 올바른 결과를 생성하는지 확인하는 함수다.
4. testPerformanceExample() :  
   성능 테스트 케이스를 작성하는 함수로 시간을 측정하는 코드를 작성하는 함수다.

3번 함수가 잘 실행 될 수 있게 준비행동을 하는 부분이 1번 함수이고 3번 함수가 실행 된 후 뒷정리를 하는 부분이 2번 함수라고 할 수 있다.

간단한 예제를 보려고 한다. 먼저 Even.swift 파일을 생성헤 다음과 같은 구조체를 정의해준다.

![Evne구조체](https://user-images.githubusercontent.com/41609708/103275959-a8f8bf00-4a08-11eb-9ce9-97f9be35aea6.jpg)

다음은 `프로젝트명Test`폴더의 swift파일의 클래스 안에 다음과 같은 테스트 예제 코드를 작성해 준다.

![test](https://user-images.githubusercontent.com/41609708/103275965-aa29ec00-4a08-11eb-80b9-8cf73d5f96ec.jpg)

`XCTAssertTrue`를 통해서 해당 숫자가 짝수이면 참, 아니면 거짓을 판별한다. 그래서 해당 number 변수의 값이 짝이면 테스트 성공, 홀수면 테스트 실패가 될 것 이다.  
테스트를 수행하기 위해서는 위 그림에서 라인 수가 적힌 부분을 보면 마름모 모양이 있을 것 이다. 이것을 클릭하게 되면 테스트를 진행하게 된다.

테스트가 성공적으로 이루어지면 아래 그림과 같고

![성공](https://user-images.githubusercontent.com/41609708/103275962-a9915580-4a08-11eb-80b1-36504d0203e5.jpg)

실패하게 되면 아래 그림과 같게 된다.

![실패](https://user-images.githubusercontent.com/41609708/103275961-a8f8bf00-4a08-11eb-9306-c0df06fca446.jpg)

---

오늘은 간단하게 Xcode 상에서 Unit Test를 진행하는 방법에 대해서 공부했다. Unit Test를 통해서 코드 작성만 중요한 것이 아니라 테스트 케이스에 대해 작성하는 것도 중요하다는 것을 알게 되었다. 물론 Unit Test를 성공적으로 끝냈다고 해서 만든 앱이 완벽하다는 것은 아니니깐 주의해야 한다!!
