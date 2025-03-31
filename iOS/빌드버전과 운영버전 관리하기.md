# 빌드버전과 운영버전 관리하기


앱 업데이트 시, `1.0.0` → `1.0.1` 과 같이 숫자를 올려가며 버전을 관리한다.
`1.0.1` 업데이트를 위한 빌드가 한 번만에 통과될 수도 있지만 보통은 그렇지 않다.
테스트 플라이트에 올리는 과정에서 오류가 나기도 하고, QA 진행 중 오류가 발견되기도 한다. 
해당 경우, 수정 후 같은 버전으로 재업로드가 필요하다. (`1.0.1.1` → `1.0.1.2`)


재빌드의 경우, 이전 빌드와 운영(업데이트)버전은 동일하지만 빌드 버전은 이전과 분명히 구분이 되어야 할 것이다. 
그렇지 않으면 오류를 수정한 빌드 버전을 구분할 방법이 없기 때문이다. 
이때 빌드 버전과 운영 버전을 구분하여 버전을 관리할 수 있다.

<br/> 

Xcode에는 두가지 버전 설정 입력란이 있다. 

<img width="513" alt="스크린샷 2025-03-31 오후 4 05 32" src="https://github.com/user-attachments/assets/6ce48bca-61a5-4767-be9a-997683ee6c2d" />

- Version
  - 이 키는 사용자 눈에 보이는 버전이다. 앱 스토어에 올라갈 버전을 작성한다.
  - `1.0.1`

- Build
  - 릴리즈가 되기 전 앱 번들의 빌드 버전이다. 개발자들의 트래킹을 위한 빌드 버전을 작성한다.
  - 해당 값은 개인에 따라 다르게 작성된다. 빌드 횟수만 작성하기도 하고, 빌드를 실시한 날짜를 작성하기도 한다.
  - `20241001` `3` `1.0.1.3`
      




각 설정란은 우측에 작성된 property list key 값을 갖는다.

- Version: **CFBundleShortVersionString**
- Build: **CFBundleVersion**

<br/>
Info.plist에서도 버전을 지정할 수 있다. 

<br/>

<img width="613" alt="image" src="https://github.com/user-attachments/assets/b9ed07ae-aca1-40f6-bbf5-089aa732edca" />
<br/><br/>

- **Bundle versions string, short → Version**
- **Bundle version → Build**


<br/><br/>

현재 EAT-SSU에서는 아래와 같이 관리하고 있다.

- **Bundle versions string, short**
    - **앱 스토어에 올라갈 버전 (2.0.0)**
- **Bundle version**
    - **앱 스토어 버전 + 빌드 횟수 (2.0.0.1 / 2.0.0.2)**
    - (빌드 횟수는 1부터 시작하는 것으로 한다)

---

https://developer.apple.com/documentation/bundleresources/information_property_list/cfbundleversion
