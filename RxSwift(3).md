# RxSwift - Scheduler, Single, Subject

저번 시간에 이어서 남은 3개에 기능인 `Single`, `Subject`, `Scheduler`에 대해 정리하려고 한다.

## Scheduler

스케줄러는 Observable 연산자 체인에 멀티스레딩을 적용하고 싶을 때 사용해 연산자나 특정 Observable을 실행하면 된다.

대표적으로 스케줄러로 동작하는 연산자는 `observeOn`과 `subscribeOn`이 있다. 하지만 `observeOn`을 더 많이 사
