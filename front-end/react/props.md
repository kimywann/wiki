# props란?

props는 부모 컴포넌트가 자식 컴포넌트에게 **값을 전달**할 때 사용하는 객체.

- properties의 줄임말.
- 자식 컴포넌트는 전달받은 props를 통해 부모가 넘긴 데이터를 활용할 수 있다.
- 읽기 전용(immutable). 자식 컴포넌트에서 직접 변경하면 안 됨.

### **📦 props 사용 방법**

#### **1.** 부모 → 자식에게 데이터 전달

```jsx
<EmailInput
  id={id}
  domain={domain}
  onChangeEmail={onChangeEmail}
  onChangeDomain={onChangeDomain}
  errors={errors}
/>
```

→ 위처럼 JSX 태그 안에서 속성처럼 props를 넘길 수 있음.

#### **2.** 자식 컴포넌트에서 받는 방법

```jsx
export default function EmailInput({
  id,
  domain,
  onChangeEmail,
  onChangeDomain,
  errors,
  idRef,
}) {
  // props를 구조 분해 할당으로 받음
}
```

## **🧱 실전 예시 정리**

#### EmailInput 컴포넌트

- 역할: 이메일(아이디 + 도메인)을 입력하는 UI를 담당
- 전달받는 props:
  - id, domain: 현재 입력된 값
  - onChangeEmail, onChangeDomain: 부모의 상태를 변경하는 함수
  - errors: 에러 메시지 객체
  - idRef: 포커스를 주기 위한 ref

📌 이 컴포넌트는 props를 받아서 상태는 직접 관리하지 않고, 입력 이벤트가 일어나면 onChangeEmail, onChangeDomain 함수를 실행해서 **부모의 상태를 바꿈**.

---

### **💡 핵심 포인트 요약**

| **포인트**                                              | **설명**                                     |
| ------------------------------------------------------- | -------------------------------------------- |
| ✅ 단방향 데이터 흐름                                   | 부모 → 자식으로 데이터 전달만 가능           |
| ✅ 자식은 상태를 갖지 않고, 부모가 상태를 갖고 변화시킴 | 상태 변경 함수(onChange 등)를 props로 전달   |
| ✅ 재사용 가능한 컴포넌트 작성                          | 같은 UI 컴포넌트를 다양한 곳에서 재활용 가능 |
| ✅ ref도 props로 전달 가능                              | 포커스 제어나 DOM 접근 시 사용               |
