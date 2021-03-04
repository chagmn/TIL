# iOS Architecture (iOS 아키텍처 패턴) (3) - MVVM

더 좋고 꾸준하게 유지보수하기 위해서는 프로그램을 구현하기 전에 적절한 아키텍처를 선정하는 것이 필요하다는 것을 알게되고 iOS 개발에 있어서 몇 가지 아키텍처 패턴에 대해 공부하려고 합니다.

!! 이 글은 아래 글을 참고해 정리했습니다.(
https://medium.com/ios-os-x-development/ios-architecture-patterns-ecba4c38de52)

---

## MVVM

MVVM은 MV종류에서 가장 강력하고 최신에 등장한 종류다. 이론적으로 MVVM은 보기에는 매우 좋아보인다. View와 Model은 이미 전과 비슷하고 중재자 역할은 View Model이 한다.

![MVVM](https://miro.medium.com/max/1400/1*uhPpTHYzTmHGrAZy8hiM7w.png)

꽤나 MVP와 유사해보인다.

- MVVM은 view controller를 View 처럼 다룬다.
- View와 Model이 독립적이다.

추가로, View와 Model 사이의 Binding이 존재하는 것이 아니라 View와 View Model 사이에 Binding이 존재한다.

View Model은 Model에서의 변화를 호출하고 자체적으로 업데이트된 Model로 업데이트하며 View와 View Model 사이에는 Binding 되어있으므로 이에따라 업데이트가 된다.

Binding을 직접 작성하지 않으려면 2가지 방법이 있다.

1. KVO 기반 라이브러리 사용.
2. RxSwift같은 Reactive Programming 사용.

사실, 최근에 MVVM이라고 하면 다들 RxSwift에 대해 많이 떠올린다. 그래서 MVVM 패턴에 대한 자세한 이야기는 RxSwift에 대해 공부할 떄 다시 한번 이야기하려고 한다.
