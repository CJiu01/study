# Firebase Analytics에서 사용자 OS 분석하기

EAT-SSU 서비스에서 커스텀 sheet를 도입하기 위해 최소 지원 버전을 15+→16+ 변경하려한다. 변경 이전에 현재 EAT-SSU 앱 사용자의 OS 버전을 알 필요가 있다. 

<img width="486" alt="스크린샷 2025-03-21 오후 3 01 13" src="https://github.com/user-attachments/assets/b8c4ab84-b37a-443d-b265-fd837d91504f" />


Firebase Analytics를 통해 현재 사용자 OS 버전을 알아보기로 한다. (앱에 Firebase Analytics가 적용되어 있어야 한다.)

<br/><br/>

## 1. 간략히 보기(top 7까지)

Firebase dashboard > 애널리틱스 > Audiences

<img width="220" alt="스크린샷 2025-03-21 오후 3 01 35" src="https://github.com/user-attachments/assets/76bdf545-4cb7-48fc-a84b-06f333c1be88" />


<br/><br/>

잠재고객 > All Users 

<img width="525" alt="스크린샷 2025-03-21 오후 3 09 39" src="https://github.com/user-attachments/assets/0b9fd18a-ad84-4687-a5b2-770bbc21da09" />


<br/><br/>

플랫폼 별 활성 사용자 > OS 및 버전 클릭

<img width="598" alt="스크린샷 2025-03-21 오후 3 10 09" src="https://github.com/user-attachments/assets/f3f16a43-1f7d-46cd-b059-ddb9732d852a" />

<br/><br/>

아래와 같이 운영체제 및 버전 별 활성 사용자가 나온다.

<img width="422" alt="스크린샷 2025-03-21 오후 3 10 25" src="https://github.com/user-attachments/assets/e6053766-ccad-4dfb-b3ca-6a395cd7ca7e" />

하지만 7이상의 사용자 지표만 볼 수 있기 때문에, 좀 더 자세한 지표를 보기 위해 `Google 애널리틱스에서 더보기` 로 가보자.

<br/><br/>

## 2. 자세히 보기(top 10까지)

해당 페이지의 우측 상단을 보면 `Google 애널리틱스에서 더보기` 버튼이 있다.
<img width="943" alt="스크린샷 2025-03-21 오후 3 12 44" src="https://github.com/user-attachments/assets/caf8ae6a-1c9d-4caf-9c9d-7ad6b3579390" />

<br/><br/>


클릭 후, 보고서 > 사용자 > 기술 > 기술 세부정보

<img width="445" alt="스크린샷 2025-03-21 오후 3 12 59" src="https://github.com/user-attachments/assets/7eb9606d-5107-4228-8a9e-84a1e200f3d8" />

<br/><br/>


+버튼 클릭 후, 플랫폼/기기 > OS 및 버전

<img width="596" alt="스크린샷 2025-03-21 오후 3 13 11" src="https://github.com/user-attachments/assets/0cdca39c-9466-4485-bae9-e06addb2eecc" />

<br/><br/>

페이지 이동하며 활성 사용자의 모든 OS 및 버전을 볼 수 있다.

<img width="489" alt="스크린샷 2025-03-21 오후 3 13 21" src="https://github.com/user-attachments/assets/5daf798d-9594-46ab-a901-3e1706ab4f2f" />

