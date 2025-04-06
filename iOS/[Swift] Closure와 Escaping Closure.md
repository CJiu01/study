# Closure와 Escaping Closure

### Closure란?

클로저란 함수의 기능을 하는 코드 블럭이다. 

- 변수에 저장하거나 다른 함수의 인자로 전달 가능
- Named Closure: 이름이 있는 함수 형태
- Unnamed Closure: 이름없이 {} 로 이루어진 함수 형태

  <br/>
  

### Escaping Closure란?

Closure의 정의에서 함수에 클로저를 매개변수로 넘길 수 있다고 하였다. Swift는 기본적으로 `non-escaping`이라고 간주한다. 전달받은 클로저가 함수 내에서만 실행되고, 함수가 끝나기전 반드시 호출된다는 의미이다. 

함수가 끝난 후에 클로저의 호출이 필요한 상황에서 클로저에 `@escaping` 붙여 사용한다.

<br/>


### 언제 필요한가?

1. **비동기 작업(Async)**
    
    ```swift
    func fetchData(completion: @escaping (String) -> Void) {
    	DispatchQueue.global().asyncAfter(deadline: .now()+1) {
    		completion("Data loaded")
    	}
    }
    ```
    
    함수 실행이 끝난 후, 1초뒤 completion 클로저가 실행된다.
    
2. **클로저를 저장하거나, 함수 외부에서 나중에 호출할 때**
    
    ```swift
    var storedClosure: (() -> Void)?
    
    func saveClosure(_ closure: @escaping () -> Void) {
    	storedClosure = closure
    }
    ```
    
    클로저를 함수 외부 변수에 저장하여, saveClosure 함수가 종료된 후에도 실행될 수 있다.
