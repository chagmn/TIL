# RxSwift

최신 개발 트랜드라고 하는 ReactiveX의 Swift 버전인 RxSwift에 대해 공부하려고 합니다. 오늘은 RxSwift의 개념에 대해 간단하게 알아보려고 합니다.

---

## Rx?

Rx는 Reactive eXtensions의 줄임말이다. 공식 페이지를 보면 Rx는 옵저버 패턴을 사용해 비동기식, 이벤트 기반의 프로그램을 구현하기 위한 라이브러리다.  
여기서 다루는 Swift를 제외하고도 많은 프로그래밍 언어를 지원한다!

## RxSwift?

RxSwift는 Reactive eXtensions 표준의 Swift 전용 구현이다. 다른 Rx 구현처럼 RxSwift의 구현 목적은 비동기 작업 및 Observable 객체 형태의 데이터 스트림과 이런 비동기 작업을 변환하고 구성하는 메소드를 쉽게 구성 할 수 있도록 하는 라이브러리다.

> 비동기 : 데이터 요청과 결과가 동시에 일어나지 않는다. 그래서 응답을 계속 기다리지 않고 다른 활동을 수행 할 수 있다.

## RxSwift의 3가지 구성요소

3가지 요소에는 `Observable`, `Operators`, `Schedulers`가 있다.

1. Observables

## 참고링크

- ReactiveX 공식 사이트 : <http://reactivex.io>
- RxSwift 공식 깃허브 : <https://github.com/ReactiveX/RxSwift>
