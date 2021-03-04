# iOS Architecture (iOS 아키텍처 패턴) (1) - MVC

더 좋고 꾸준하게 유지보수하기 위해서는 프로그램을 구현하기 전에 적절한 아키텍처를 선정하는 것이 필요하다는 것을 알게되고 iOS 개발에 있어서 몇 가지 아키텍처 패턴에 대해 공부하려고 합니다.

!! 이 글은 아래 글을 참고해 정리했습니다.(
https://medium.com/ios-os-x-development/ios-architecture-patterns-ecba4c38de52)

---

1. 아키텍처 패턴이란?  
   간단하게 프로그램의 구조라고 생각한다. 위키에서는 소프트웨어 내에서의 공통적인 발생 문제들을 해결하기 위한 일반적인 해결 방법이라고 설명하고 있다.

2. 왜 필요한가?  
   프로그램은 제대로 작성만 된다면 실행이 가능하다. 하지만 이런 프로그램들은 유지보수에 굉장히 많은 비용이 들어가며 실력있는 개발자가 보기에는 가독성이 떨어진다고 볼 수 있다.

3. 좋은 아키텍처는 무엇인가?

- 균형잡힌 분배 (Balanced Distribution)

  - 객체지향 원칙 중 Single Responsibility에 기반. -> 하나의 객체는 하나의 역할만 갖는다.
  - 모듈(클래스)들의 독립성이 떨어지면 테스트가 어렵다.

- 테스트 가능 (Testablity)

  - 테스트 중 발생하는 이슈를 사전에 발견하기 위한 단계다.

- 사용하기 쉬운지 (Easy of Use)

  - 개발 속도와 관련이 있다.

- 단방향성 데이터 흐름 (Unidirectional Data Flow)
  - 코드를 쉽게 이해할 수 있게 하며 쉬운 디버깅을 제공한다.
  - 에러가 발생하면 원인을 찾기 힘들어 지는 공유 자원의 사용도 피해야한다.

4가지 조건을 충족시키는 완변한 아키텍처는 존재하지 않는다. 그러니깐 자신의 프로젝트 성격에 맞춰서 적절한 아키텍처 도입이 필요하다.

iOS에서는 4가지 조건 중 균형잡힌 분배를 위해서 크게 3가지로 나누어 코딩이 진행된다.

- Model : 데이터 조작이 일어나고 이를 담당하는 부분.
- View : 사용자에게 보여주는 시각적인 부분으로 UI에 해당.
- Controller / Presenter / ViewModel : 이 부분은 Model과 View 사이의 중재자로 View를 통해 발생한 사용자의 액션에 따라 동작하며, Model에 값의 조정을 요청하며 Model 값의 변화에 맞게 View를 갱신하는 역할.

그래서 iOS에서 가장 많이 사용되는 아키텍처 패턴이 MVC, MVP, MVVM가 있으며 하나씩 살펴보려고 한다.

---

## MVC

가장 유명하며 처음 접하는 개발자들이 자연스럽게 사용하는 아키텍처이다. MVC 아키텍처는 전통적으로 사용하던 방식과 애플에서 제시한 방식으로 나누어 진다. 여기서는 애플이 제시한 MVC 방식을 보려고 한다.

애플이 제시한 MVC 방식은 Cocoa MVC 라고 불린다. Controller는 View와 Model의 중재자로 View와 Model의 직접적인 연결을 막는다. 이 점이 전통적인 방식보다 높은 독립성의 보장을 기대하고 있다.

![Cocoa MVC](https://miro.medium.com/max/1000/1*c0aGaDNX41qu6e8E4OEgwQ.png)

위 그림을 보면 View와 Model 사이에는 관계가 없어 마치 독립성이 보장되는 것 처럼 보일 수도 있다. 하지만, 실제는 그림과는 많이 다르다고 한다.

실제 Cocoa MVC 아키텍처에서 Controller의 역할은 `UIViewController`가 담당한다. 그리고 `UIViewController`는 View를 소유하며 View들의 생명주기와 강하게 연결된다. 이 말은 View와 Controller의 분리가 쉽지 않고 Controller의 재사용이 어려워지며 마찬가지로 연관되어 있는 View의 재사용도 어려워진다.

View와 Controller의 분리가 쉽지않고 강하게 연결되어 있으면 테스트 과정도 힘들다. 결국엔 독립적인 부분은 Model뿐이다.

View에서의 사용자의 액션과 메소드, `UIViewController`에서 발생하는 액션들로 (Delegation, 통신 등) Controller의 크기는 점점 커지고 이를 Massive ViewController 라고 부른다.

실제의 Cocoa MVC 형태를 그림으로 보면 다음과 같다.

![실제 Cocoa MVC](https://camo.githubusercontent.com/8aa2dba7aa59811552c5eb3cd7e444dd531010c570fee6461eda0e128f936187/68747470733a2f2f63646e2d696d616765732d312e6d656469756d2e636f6d2f6d61782f313630302f312a506b576a4455306a71474a4f42393732634d73726e412e706e67)

커진 `UIViewController`를 줄이는 행위인, View Controller Offloading은 iOS 개발자들에게 중요한 과제가 됬다.

```swift
import UIKit

// Model
struct Person{
    let firstName: String
    let lastName: String
}

// View + Controller
class GreetingViewController: UIViewController{
    var person: Person!

    var showGreetingButton: UIButton = {
        let button = UIButton()
        button.setTitle("Click", for: .normal)
        button.addTarget(self, action: #selector(didTapButton(sender:)), for: .touchUpInside)
        return button
    }()

    var greetingLabel: UILabel = {
       let label = UILabel()
        label.textColor = UIColor.black
        return label
    }()

    override func viewDidLoad(){
        super.viewDidLoad()
        self.view.addSubview(showGreetingButton)
        self.view.addSubview(greetingLabel)
    }

    @objc func didTapButton(sender: UIButton){
        let greeting = "Hi" + " " + self.person.firstName + " " + self.person.lastName
        self.greetingLabel.text = greeting
    }
}

let model = Person(firstName: "Kim", lastName: "JangGu")
let vc = GreetingViewController()
vc.person = model
```

위 코드에서 View에 해당하는 `showGreetingButton`, `greetingLabel`이 Controller 안에 위치하고 이들의 액션인 `didTapButton` 또한 Controller 안에 위치한다.

그럼, MVC 아키텍처는 언급했던 아키텍처의 기준에 얼마나 부합할까?

- Distribution : View와 Model은 분리되었지만, View와 Controller는 강하게 연결되어 있다.
- Testability : View와 Controller가 강하게 연결되어 있어서 Model만 테스트를 진행 할 수 있다.
- Easy of Use : 가장 적은 양의 코드를 필요하며 경험이 적은 개발자들도 쉽게 유지보수 할 수 있다.

아키텍처를 잘 모를 때 사용하기 쉬운 패턴이지만 작은 프로젝트여도 많은 유지보수 비용이 들어간다.
