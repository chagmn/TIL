# RxSwift

최신 개발 트랜드라고 하는 ReactiveX의 Swift 버전인 RxSwift에 대해 공부하려고 합니다. 오늘은 RxSwift의 개념에 대해 간단하게 알아보려고 합니다.

---

## Rx?

Rx는 Reactive eXtensions의 줄임말이다. 공식 페이지를 보면 Rx는 옵저버 패턴을 사용해 비동기식, 이벤트 기반의 프로그램을 구현하기 위한 라이브러리다.  
여기서 다루는 Swift를 제외하고도 많은 프로그래밍 언어를 지원한다!

## RxSwift?

RxSwift는 Reactive eXtensions 표준의 Swift 전용 구현이다. 다른 Rx 구현처럼 RxSwift의 구현 목적은 비동기 작업 및 Observable 객체 형태의 데이터 스트림과 이런 비동기 작업을 변환하고 구성하는 메소드를 쉽게 구성 할 수 있도록 하는 라이브러리다.

> 비동기 : 데이터 요청과 결과가 동시에 일어나지 않는다. 그래서 응답을 계속 기다리지 않고 다른 활동을 수행 할 수 있다.

## 왜 RxSwift를 사용할까?

1. MVVM패턴과 관련 :  
   MVVM패턴은 데이터 바인딩을 제공하는 플랫폼에서 만들어진 이벤트 중심 프로그램을 위한 아키텍쳐인데 RxSwift가 연관성이 높다.

2. 순수하게 비동기적인 프로그래밍을 하면? :
   애플이 제공하는 Delegate패턴을 그대로 사용해 개발자가 비동기 실행 코드를 이해하기 힘들다. 하지만 RxSwift를 사용하면 코드 이해가 쉬워진다.

## 참고링크

- ReactiveX 공식 사이트 : <http://reactivex.io>
- RxSwift 공식 깃허브 : <https://github.com/ReactiveX/RxSwift>
