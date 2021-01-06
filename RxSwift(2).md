# RxSwift - Observable, Operators

ReactiveX 공식 페이지 Docs메뉴에 보면 5가지 기능을 소개해준다. 오늘은 이 5가지(`Observable`, `Operators`, `Single`, `Subject`, `Scheduler`) 중 `Observable`과 `Operators`에 대해 정리하려고 한다.

## Observable

ReactiveX에서는 옵저버에 의해서 정해진 순서에 따라 병렬로 코드가 실행되고 결과는 나중에 연산된다. 이러한 방식은 하나의 코드 블럭이 실행 결과를 리턴할 때까지 기다리지않고 다음 코드 블럭을 실행시켜 프로그램 실행 시간을 단축시킨다는 장점도 있다. 공식문서에서는 비동기 프로그램과 설계 모델을 이야기할 때 "옵저버는 Observable을 구독한다" 라고 표현한다.

옵저버는 `Subscribe`메서드를 통해서 Observable을 구독하고 `onNext`, `onError`, `onCompleted`라는 메소드를 구현하게 된다.

- `onNext` : Observable이 배출하는 값을 파라미터로 전달받는다.

- `onError` : Observable이 원하던 값이 아니거나 오류가 발생하면 이 메서드를 호출하고 오류 정보 객체를 파라미터로 전달받고 `onNext`나 `onCompleted`메서드는 호출되지 않는다.

- `onCompleted` : Observable은 제일 마지막에 이 메소드를 호출한다.

> `onNext`는 0번이상 호출 가능, 그 다음 `onError`나 `onCompleted` 중 하나를 마지막에 호출.

## Operators

연산자는 Observable 상에서 동작하고 Observable을 리턴한다. 이러한 방식은 연산자들을 연속으로 호출 가능한 연산자 체인을 제공한다. 특히, 연산자들이 연속으로 있는 경우 호출 순서에 따라서 실행 결과 값이 달라질 수 있다.

### 카테고리 별 연산자

카테고리 별 주요 연산자들만 설명하고 자세한 내용은 공식 문서를 참고하면 좋을 것 같다. 공식 문서를 보면 어떤 식으로 연산자가 작동하는지 연산자마다 그림으로 쉽게 표현되어있다.

#### Observable 생성

새로운 Observable을 생성하는 연산자

- `Just` : 객체 하나 또는 객체 집합을 Observable로 변환
- `From` : 다른 객체나 자료구조를 Observable로 변환

#### Observable 변환

Observable이 반환하는 데이터를 변환하는 연산자

- `Map` : Observable이 반환하는 데이터에 함수를 적용

#### Observable 필터링

Observable에서 선택적으로 데이터를 반환하는 연산자

- `Filter` : 조건을 만족하는 데이터를 반환
- `First` : 맨 첫 번째나 조건을 만족하는 첫 번째 데이터만 반환

#### Observable 결합

여러 개의 Observable들을 하나로 결합하는 연산자

- `Merge` : 다수의 Observable들이 반환하는 데이터를 합쳐 하나로 만듬

#### 오류 처리

- `Catch` : 오류를 무시하고 반환되는 데이터를 진행해 onError로부터의 오류를 복구
- `Retry` : onError가 발생할 경우 오류없이 동작하기를 기대하면서 다시 진행

#### Observable 유틸리티

Observable과 함께 동작하는 연산자

- `Do` : Observable의 생명주기에서 발생하는 여러 이벤트에서 실행될 액션을 등록
- `ObserveOn` : 옵저버가 어느 스케줄러 상에서 Observable을 관찰할지 명시
- `Subscribe` : Observable이 반환하는 데이터와 알림을 기반으로 동작
- `SubscribeOn` : Observable을 구독할 때 사용할 스케줄러를 명시

## 참고

- ReactiveX 공식 홈페이지 :
  http://reactivex.io/documentation/ko/observable.html
