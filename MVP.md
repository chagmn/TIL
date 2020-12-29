# iOS Architecture (iOS 아키텍처 패턴) (2) - MVP

더 좋고 꾸준하게 유지보수하기 위해서는 프로그램을 구현하기 전에 적절한 아키텍처를 선정하는 것이 필요하다는 것을 알게되고 iOS 개발에 있어서 몇 가지 아키텍처 패턴에 대해 공부하려고 합니다.

!! 이 글은 아래 글을 참고해 정리했습니다.(
https://medium.com/ios-os-x-development/ios-architecture-patterns-ecba4c38de52)

---

## MVP

![MVP](https://miro.medium.com/max/1400/1*hKUCPEHg6TDz6gtOlnFYwQ.png)

위 그람은 애플의 MVC와 비슷해보이지만 MVP다. 하지만, 둘은 다르다.

MVP에서 `UIView`나 `UIViewController` 둘 다 View에 해당한다. 이 부분이 MVC와 다른 부분인데, MVC에서는 `UIViewController`는 Controller에 해당해서 View와의 강한 연결을 갖고 있었다. MVP에서는 View로 분류하는 대신에 Presenter라는 것이 등장했다.

Presenter는 View의 생명 주기에 영향을 주지 않고 레이아웃 코드도 Presenter에 존재하지 않는다. 또한 View의 데이터와 상태에 맞게 View를 갱신하는 역할을 한다. 다시 말해서 Presenter는 Model으로 부터 업데이트 된 데이터를 전달 받아 View를 갱신하는 역할을 한다.

MVP 아키텍처를 코드로 구현해볼 수 있다.

```swift
import UIKit

// Model
struct Person{
    let firstName: String
    let lastName: String
}

// View Protocol
protocol  GreetingView {
    func setGreeting(greeting: String)
}

// Presenter Protocol
protocol GreetingViewPresenter {
    init(view: GreetingView, person: Person)
    func showGreeting()
}

// Presenter
class GreetingPresenter: GreetingViewPresenter {
    var view: GreetingView
    let person: Person

    required init(view: GreetingView, person: Person) {
        self.view = view
        self.person = person
    }

    // 3. View 갱신
    func showGreeting() {
        let greeting = "Hi" + " " + self.person.firstName + " " + self.person.lastName
        self.view.setGreeting(greeting: greeting)
    }
}

// View
class GreetingViewController: UIViewController, GreetingView {
    var presenter: GreetingViewPresenter!

    var showGreetingButton: UIButton = {
       let button = UIButton()
       button.setTitle("Click", for: .normal)
       return button
    }()

    var greetingLabel: UILabel = {
       let label = UILabel()
       label.textColor = UIColor.black
       return label
    }()

    func setGreeting(greeting: String) {
        self.greetingLabel.text = greeting
    }


    override func viewDidLoad() {
        super.viewDidLoad()
        self.view.addSubview(showGreetingButton)
        self.view.addSubview(greetingLabel)
        showGreetingButton.addTarget(self, action: #selector(didTapButton(sender:)), for: .touchUpInside)

    }

    // Presenter에게 액션을 전달
    @objc func didTapButton(sender: UIButton){
        self.presenter.showGreeting()
      }

}

let model = Person(firstName: "Kim", lastName: "MVP")
let view = GreetingViewController()
let presenter = GreetingPresenter(view: view, person: model)
view.presenter = presenter
```

코드를 보면 View는 Presenter를 `presenter` 변수에서 소유하고 있어서 참조에 의한 1:1 의존성을 벗어나지 못했고 액션을 통해서 Presnter에게 액션을 전달한다.

MVP도 좋은 아키텍처의 기준에 얼마나 부합하는지 보자.

- Distribution : Model과 View의 의존성은 해결했지만 참조에 의한 View와 Presenter의 의존성이 존재한다.
- Testability : 각각의 요소를 독립적으로 테스트하기에 용이하다.
- Easy of Use : Presenter의 추가와 프로토콜의 추가로 코드가 MVC에 비해 길다.
