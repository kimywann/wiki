## 인증과 인가에 대해 설명해주세요.

인증(Authentication)은 **"사용자가 누구인지 확인하는 과정"** 이고, 인가(Authorization)는 **"사용자가 특정 자원에 접근할 권한이 있는지 확인하는 과정"** 입니다.

먼저, 인증은 **사용자의 신원을 검증하는 과정입니다.** 예를 들어, 웹사이트에 로그인할 때 아이디와 비밀번호를 입력받아 해당 사용자가 누구인지 검증하는 것이 이에 해당합니다. 인증 방식에는 비밀번호 기반 인증, 생체 인증, OTP 인증 등이 있습니다. 또한, 최근에는 보안 강화를 위해 MFA(다중 요소 인증)도 널리 사용되고 있습니다.

반면, 인가는 인증을 통해 신원이 식별된 사용자가 **특정 리소스에 접근할 수 있는 권한을 갖고 있는지 확인하는 과정입니다.** 예를 들어, 회사 내부 시스템에서 일반 직원은 고객 데이터를 조회할 수 없지만, 관리자 계정은 조회할 수 있도록 설정하는 것이 인가의 한 예입니다. 이 사례에서 일반 직원이 고객 데이터에 접근하지 못하는 이유는 인증에는 성공하지만, 권한이 부족하여 인가에 실패하기 때문입니다.

## [](https://www.maeil-mail.kr/question/192#%EC%A0%91%EA%B7%BC-%EC%A0%9C%EC%96%B4-%EB%B0%A9%EC%8B%9D%EC%97%90%EB%8A%94-%EC%96%B4%EB%96%A4-%EB%B0%A9%EC%8B%9D%EB%93%A4%EC%9D%B4-%EC%9E%88%EB%82%98%EC%9A%94-)접근 제어 방식에는 어떤 방식들이 있나요? 🤔

대표적인 접근 제어 방식으로는, RBAC(Role-Based Access Control), ABAC(Attribute-Based Access Control), ReBAC(Relationship-Based Access Control)이 있습니다.

**RBAC**는 사용자의 역할에 따라 접근 권한을 부여하는 방식으로, 조직 내에서 필요한 역할들을 생성하고 각 역할 별로 어떤 자원에 접근이 가능하며 어떤 행동이 가능한지를 설정합니다. **ABAC**는 사용자의 속성을 기반으로 접근 권한을 결정하는 방식으로, 보다 세밀한 제어가 가능합니다. **ReBAC**는 사용자 및 자원 간의 관계를 기반으로 접근 권한을 결정하는 방식입니다.

## [](https://www.maeil-mail.kr/question/192#%EC%B6%94%EA%B0%80-%ED%95%99%EC%8A%B5-%EC%9E%90%EB%A3%8C%EB%A5%BC-%EA%B3%B5%EC%9C%A0%ED%95%A9%EB%8B%88%EB%8B%A4)추가 학습 자료.

- [[okta] 인증과 인가 비교](https://www.okta.com/kr/identity-101/authentication-vs-authorization/)
- [[okta] RBAC와 ABAC 의 특징 비교: 정의 및 사용 사례](https://www.okta.com/kr/identity-101/role-based-access-control-vs-attribute-based-access-control/)
- [[Permit] Understanding Relationship Based Access Control (ReBAC)](https://www.youtube.com/watch?v=xCqpxiPXnCk)