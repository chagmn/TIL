# RxSwift

ReactiveX 공식 페이지 Docs메뉴에 보면 5가지 기능을 소개해준다. 오늘은 이 5가지(`Observable`, `Operators`, `Single`, `Subject`, `Scheduler`)에 대해 정리하려고 한다.

## Observable

ReactiveX에서는 옵저버에 의해서 정해진 순서에 따라 병렬로 코드가 실행되고 결과는 나중에 연산된다. 이러한 방식은 하나의 코드 블럭이 실행 결과를 리턴할 때까지 기다리지않고 다음 코드 블럭을 실행시켜 프로그램 실행 시간을 단축시킨다는 장점도 있다. 공식문서에서는 비동기 프로그램과 설계 모델을 이야기할 때 "옵저버는 Observable을 구독한다" 라고 표현한다.

옵저버는 `Subscribe`메서드를 통해서 Observable을 구독하고 `onNext`, `onError`, `onCompleted`라는 메소드를 구현하게 된다.

- `onNext` : Observable이 배출하는 값을 파라미터로 전달받는다.

- `onError` : Observable이 원하던 값이 아니거나 오류가 발생하면 이 메서드를 호출하고 오류 정보 객체를 파라미터로 전달받고 `onNext`나 `onCompleted`메서드는 호출되지 않는다.

- `onCompleted` : Observable은 제일 마지막에 이 메소드를 호출한다.

> `onNext`는 0번이상 호출 가능, 그 다음 `onError`나 `onCompleted` 중 하나를 마지막에 호출.

## 참고
