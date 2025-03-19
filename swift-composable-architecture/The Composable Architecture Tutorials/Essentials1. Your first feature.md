
<img width="476" alt="스크린샷 2025-03-19 오후 12 49 20" src="https://github.com/user-attachments/assets/7dd918f0-4a54-4b5e-82e6-85370797af4c" />
<br/><br/>

# Tutorial1. **Your first feature**

이번 챕터의 목표는 아래와 같다.

- Reducer 구현 방법 이해
- 구현한 Reducer를 SwiftUI view와 바인딩

구현에 들어가기 전, Reducer가 무엇이고 어떤 것을 구현해야 하는지 간략하게 살펴보자.

리듀서(Reducer) 는 어떤 행동(Action)이 주어졌을 때, 현재 상태(State)를 다음 상태(State)로 변화시키는 방법을 가지고 있다. 또한 리듀서는 실행할 수 있는 이펙트(Effect)를 반환해야 한다. 함수의 기능을 하는 구조체라고 생각하면 이해가 편하다.

<br/><br/>


## section1) Create a reducer

`CounterFeature.swift`

먼저 리듀서를 생성해보겠다. 리듀서는 뷰와 분리하여 개발함으로써 재사용과 테스트에 더 용의하게 할 것이다.

**step1.**

- **`@Reducer`**

`CounterFeature` 구조체를 정의한다. 

이때 매크로가 붙은 리듀서(`@Reducer`)를 표기해 줄 것이다.

```swift
import ComposableArchitecture

@Reducer
struct CounterFeature {
  
}
```

매크로가 붙은 리듀서는 우리에게 추가적인 것들을 제공하지만, 우선 타입이 리듀서 프로토콜을 준수하도록 확장한다는 것만 알고 가자.

**step2.**

- State
- Action

이번 스텝에서는 State와 Action을 정의할 것이다. 단어 의미 그대로 해석하면 된다. 
State는 행동이 수행되는데 필요한 상태들이 정의되어 있다. Action에는 수행할 수 있는 모든 행동에 대해 정의되어 있다.

```swift
import ComposableArchitecture

@Reducer
struct CounterFeature {
  
  @ObservableState
  struct State {
  
  }
  
  enum Action {
  
  }
  
}
```

State 구조체에는 `@ObservableState` 매크로를 추가하였는데, 이는 Observable 프로토콜을 채택하여 State를 관찰 대상으로 지정하기 위해서이다.

좀 더 풀어서 설명하자면, State가 바뀔 때마다 이를 View가 인지하고 갱신되어야한다. 이를 위해 State를 관찰대상으로 두고 값이 바뀌는지 관찰하는 것이다.

**step3.**

- 변수 생성

```swift
@ObservableState
struct State {
    var count = 0
}

enum Action {
    case decrementButtonTapped
    case incrementButtonTapped
}
```

행동을 정의할 때에는 사용자의 행동을 직관적으로 담는 것이 좋다.(ex. `incrementButtonTapped`) 행동에 대한 로직을 변수명으로 지정하는 것을 지양하자.(ex. `incrementCount`)

**step4.**

- body property

`Reduce` 리듀서는 body를 정의함으로써 시행될 수 있다. body 내부에서 리듀서를 나열하여 사용자의 동작에 따라 현재 값을 다음 값으로 바꿔주고, 실행할 이펙트를 리턴할 것이다. 여기서 state는 `inout` 으로써 제공되어 즉각적인 반영이 가능하다.

```swift
var body: some ReducerOf<Self> {
    Reduce { state, action in
        switch action {
        case .decrementButtonTapped:
            
        case .incrementButtonTapped:
        
        }
    }
}
```

**step5.**

각 행동에 따른 `state`와 `리턴할 Effect`를 작성해준다. 

해당 케이스에서는 실행할 이펙트가 존재하지 않기 때문에 `.none` 을 리턴해 줄 것이다. 

```swift
var body: some ReducerOf<Self> {
        Reduce { state, action in
            switch action {
            case .decrementButtonTapped:
                state.count -= 1
                return .none
            case .incrementButtonTapped:
                state.count += 1
                return .none
            }
        }
    }
```

여기까지 매우 간단한 Composable Architecture를 구현해보았다. 

<aside>
💡

**리듀서는 상태(state)와 액션(action)을 포함한 구조체이다.**

</aside>

이밖에도 effect 방출, 리듀서에서 의존성 주입, 리듀서 합성 등 많은 것들이 있지만 우선은 여기까지다.

이제 지금까지 구현한 것들을 뷰에 나타내보는 작업을 해보겠다.

### section2) Integrating with SwiftUI

`CounterFeature.swift`

리듀서로 간단한 기능을 만들었으니, 이를 SwiftUI 뷰에 붙이는 작업을 해볼 것이다. 어떻게 붙일 수 있을까?

이를 위해 우리는 **`Store`** 라는 개념을 알아볼 것이다.

**step1.**

- CounterView
- store

먼저 store를 만들어보자. store는 **`StoreOf<CounterFeature>`** 타입으로 생성할 것이다.

```swift
import SwiftUI

struct CounterView: View {
  **let store: StoreOf<CounterFeature>**

  var body: some View {
    EmptyView()
  }
}
```

store를 만든다고 했는데 왜 **`StoreOf` 타입이냐?**

**`StoreOf` 는 typealias를 통해 정의된 새로운 별칭이고, 기존의 타입을 보면 Store로 정의되어 있다.**

```swift
let store: Store<Feature.State, Feature.Action>
```

하지만 매번 정의하기 번거로우니 typealias를 통해 **`StoreOf` 라는 새로운 이름을 붙인 것이다.**

![스크린샷 2024-11-10 오후 6.01.58.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/777e0746-8fb3-40a3-a090-852d9384e2de/f99e502f-dfc1-4f0c-98de-b703085f3569/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2024-11-10_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_6.01.58.png)

이로써, 위에서 보았던 형식의 선언이 가능한 것이다.

```swift
let store: StoreOf<Feature>
```

다시 아래의 코드로 돌아와보자.

<> 안에는 store가 관리할 기능을 넣어주면 된다. 우리는 앞에서 만들어놓았던 **CounterFeature 모듈(리듀서 구조체)을 넣어줄 것이다.**  

```swift
**let store: StoreOf<CounterFeature>**
```

정리하면  **`CounterFeature`의 상태와 액션을 관리할 수 있는 store 인스턴스를 만드는 코드이다.**

Tips) let으로 store를 선언 가능하다. 그리고 앞에서 선언하였던 **`ObservableState()`** 매크로를 통해 **`store`** 내부의 데이터의 변화를 자동으로 관찰가능하다.

**step2.**

- view

count 텍스트와 -,+ 버튼이 있는 뷰를 만들어준다.

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/777e0746-8fb3-40a3-a090-852d9384e2de/3f9f9554-4f2b-44d2-8243-7606a16be9a6/image.png)

```swift
var body: some View {
    VStack {
        Text("0")
            .font(.largeTitle)
            .padding()
            .background(Color.black.opacity(0.1))
            .cornerRadius(10)
        HStack {
            Button("-") {
            }
            .font(.largeTitle)
            .padding()
            .background(Color.black.opacity(0.1))
            .cornerRadius(10)
            
            Button("+") {
            }
            .font(.largeTitle)
            .padding()
            .background(Color.black.opacity(0.1))
            .cornerRadius(10)
        }
    }
}
```

**step3.**

- **`send(_:)`**

이제 기본적인 뷰 설정이 완료되었으니, store에서 상태를 읽고, store에 액션을 전송해보겠다.

먼저 store의 count를 Text로 보여줄 것이다. store 내부 데이터에 변화가 발생하면 이는 추적되어 text에 업데이트 될 것이다.

send( :) 메소드를 통해 store에 액션을 전달할 수 있다.

```swift
var body: some View {
	  VStack {
	      **Text("\(store.count)")**
	          .font(.largeTitle)
	          .padding()
	          .background(Color.black.opacity(0.1))
	          .cornerRadius(10)
	      HStack {
	          Button("-") {
	              **store.send(.decrementButtonTapped)**
	          }
	          .font(.largeTitle)
	          .padding()
	          .background(Color.black.opacity(0.1))
	          .cornerRadius(10)
	
	          Button("+") {
	              **store.send(.incrementButtonTapped)**
	          }
	          .font(.largeTitle)
	          .padding()
	          .background(Color.black.opacity(0.1))
	          .cornerRadius(10)
	      }
	  }
}
```

**step4.**

- `#Preview`

프리뷰를 추가할 것이다. CounterView를 생성할 때에는 store를 주입해주어야 한다. (정확한 타입으로는 **`StoreOf<CounterFeature>`** 이 될 것이다)

```swift
#Preview {
    CounterView(
        store: Store(initialState: CounterFeature.State()) {
            CounterFeature()
        }
    )
}
```

조금 더 자세히 살펴보자. 우선 CounterView의 파라미터로 store를 전달해야하기 때문에 store 를 초기화하고 있는 것까지는 이해가 간다.

그리고 store의 초기화 방식은 아래와 같은데, 이 부분에 대해서 좀 더 자세히 볼 것이다.

```swift
Store(initialState: CounterFeature.State()) { CounterFeature() }
```

Store의 definition을 보자.

![스크린샷 2024-11-10 오후 9.25.08.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/777e0746-8fb3-40a3-a090-852d9384e2de/6b39e613-ba59-4e78-b0e0-350fa1da4e4c/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2024-11-10_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_9.25.08.png)

파라미터로 두 항목이 존재한다.

- initialState
- reducer

하나씩 살펴보자.

1. initialState

initialState 매개변수는 Store가 관리할 초기 상태를 지정한다.

우리가 작성한 코드를 보면 `CounterFeature.State()` 를 전달하고 있는데, 이는 `CounterFeature` 에 정의된 상태의 초기값을 생성하는 코드이다. Section1에서 우리는 구조체로 State를 생성했기 때문에 `State()` 와 같이 초기화가 가능한 것이다. 

1. reducer

reducer 매개변수는 Store가 사용할 리듀서 인스턴스를 지정한다. 이 매개변수는 `() → Reducer` 형식으로 전달되고, `CounterFeature` 의 비즈니스 로직과 상태 변화를 전달하는 리듀서 역할을 한다.

우리가 작성한 코드를 보면, reducer의 인자로 클로저를 전달하고 있는 것을 볼 수 있다. (더 정확히는 trailing closure이다)

```swift
{ CounterFeature() }
```

클로저 `{ CounterFeature() }`  는 `() → Reducer` 타입이라고 할 수 있다.

- 매개변수를 받지 않고 `()`
- `Reducer` 타입의 값을 반환한다.

### 왜 `() → Reducer` 형태로 전달할까? 에 대한 나의 생각은

리듀서와 같은 큰 객체를 미리 생성하여 전달하는 것보다 클로저 형태로 전달함으로써 필요할 때 그 즉시 생성 가능하도록 하기 위한 목적이 아닐까? 이렇게 하면 Store가 이 클로저를 호출할 때마다 새로운 리듀서를 얻을 수 있을 것이다.

step4 가 조금 길어졌는데 Store의 초기화 과정을 아래와 같이 정리해 볼 수 있을 것 같다.

> **`Store`**를 `CounterFeature`의 상태와 리듀서를 기반으로 초기화하여, 이후 **`Store`**를 통해 `CounterFeature`의 상태를 읽고 업데이트할 수 있도록 설정한다.
> 

step5.

번외로,

여기서! `CounterFeature()` 를 주석처리하면 어떻게 될까?

```swift
#Preview {
    CounterView(
        store: Store(initialState: CounterFeature.State()) {
//            CounterFeature()
        }
    )
}
```

store를 생성할 때 리듀서가 전달되지 않으면 어떻게 될지를 생각해보면 된다.

리듀서에는 모든 기능의 로직과 액션이 담겨있다. 따라서 버튼을 눌러도 액션이 동작하지 않을 것이며, 상태도 변하지 않을 것이다. (초기값은 설정된다.)

로직이나 동작을 제외하고 오로지 디자인적인 요소만 테스트하고 싶다면 이렇게 활용할 수 있다.

이번 섹션은 여기까지다.

이번 섹션에서는 Composable Architecture와 SwiftUI view를 합치는 작업을 해보았다.

다음 섹션에서는 이것이 실제 app에서 구동되려면 어떻게 해야하는지 알아볼 것이다.

### section3) Integrating into the app

`CounterApp.swift`

**step1.**

- entry point

CounterApp의 진입점을 `CounterView`로 바꿔준다. 그리고 preview에서 했던 것과 같이 `CounterView` 를 생성해준다.

```swift
import ComposableArchitecture
import SwiftUI

@main
struct CounterApp: App {
    var body: some Scene {
        WindowGroup {
            CounterView(
                store: Store(initialState: CounterFeature.State()) {
                    CounterFeature()
                }
            )
        }
    }
}
```

앞에서 자세히 설명했으므로, 여기서는 넘어가겠다.

**step2.**

- store의 생성과 관리

결론부터 말하자면 store는 앱 내부에서 **한 번만** 생성되어야 한다. 

이를 강제하기 위해 step1에서 작성했던 코드를 아래와 같이 수정할 것이다.

```swift
@main
struct CounterApp: App {
    static let store = Store(initialState: CounterFeature.State()) {
        CounterFeature()
    }
    
    var body: some Scene {
        WindowGroup {
            CounterView(store: CounterApp.store)
        }
    }
}
```

하나씩 살펴보자.

- **단일 Store 인스턴스 사용**

앱의 Store는 @main 앱 구조 내에서 한 번만 정의해, 상태와 액션 처리를 일관되게 유지할 수 있다. 

- **루트 `WindowGroup`에서 `Store` 제공**

WindowGroup 내부의 루트뷰인 CounterView에 Store를 전달하고 있다. 이를 통해 루트뷰와 그 하위 뷰들이 모두 동일한 Store를 공유할 수 있게 된다.

- **정적 변수 사용의 이유**

`static` 키워드를 사용하여 store를 정의해주었다. 이를 통해 앱 어디에서나 `CounterApp.store` 로 접근할 수 있다. 또, 이는 모든 뷰가 같은 store가 참조되도록 보장하는 역할도 한다.

**step3.**

- `_printChanges(_:)`

리듀서가 처리하는 모든 액션과 액션을 수행한 후에 상태가 어떻게 변화하는지 로그를 찍어주는 메서드이다. 

```swift
static let store = Store(initialState: CounterFeature.State()) {
    CounterFeature()
        ._printChanges()
}
```

![스크린샷 2024-11-11 오전 1.01.14.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/777e0746-8fb3-40a3-a090-852d9384e2de/890b8357-53f0-4b00-92eb-5e828b2b0cc1/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2024-11-11_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_1.01.14.png)
