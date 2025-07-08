# React Hooks & Custom Hook

_React의 상태 관리와 훅 사용의 기본 규칙 정리_

---

## **🔄 React의 데이터 흐름: 단방향 바인딩**

- **React는 단방향 흐름을 갖는다.**
  → **부모 → 자식으로만 props 전달 가능**
- 자식 컴포넌트에서 useState로 상태를 선언하면,
  부모 컴포넌트가 그 값을 알 수 없다 ❌
- 따라서 **공통으로 써야 할 상태는 부모 컴포넌트에서 선언하고, 자식에 props로 넘겨줘야 한다.**
  예:

```jsx
// 부모에서 선언
const [email, setEmail] = useState("");

// 자식에서 props로 받음
<EmailInput value={email} onChange={setEmail} />;
```

## **🧩 React Hook의 사용 규칙 (Rules of Hooks)**

> **Hooks는 함수 컴포넌트 안에서만, 최상위에서만 사용해야 한다!**

### **✅ 올바른 사용 예**

```jsx
function Component() {
  const [value, setValue] = useState(""); // 컴포넌트 최상단에서 선언
}
```

### **❌ 잘못된 사용 예**

```jsx
if (condition) {
  const [value, setValue] = useState(""); // ❌ 조건문 안에서 사용 X
}

function handleClick() {
  const [value, setValue] = useState(""); // ❌ 이벤트 핸들러 안에서 사용 X
}
```

### **이유:**

- 훅은 **렌더 순서를 보장**해야 정상 작동함.
  조건문, 루프, 이벤트 안에서 쓰면 순서가 깨져서 오류 발생.

---

## **🛠 Custom Hook 이란?**

- 여러 컴포넌트에서 공통적으로 쓰는 상태 로직을 분리한 함수
- 이름은 use로 시작해야 함
- 내부에서 useState, useRef, useEffect 같은 훅들을 자유롭게 사용할 수 있음

---

## **🧪 Custom Hook 반환 방식**

### **1. 배열로 반환**

```jsx
// useInput.js
export default function useInput() {
  const [value, setValue] = useState("");
  const ref = useRef(null);
  const onChange = (e) => setValue(e.target.value);
  return [value, ref, onChange];
}

// 사용
const [nickname, nicknameRef, onChangeNickname] = useInput();
```

- 간단하고 짧게 쓸 수 있음
- 하지만 순서를 기억해야 하므로 가독성이 떨어질 수 있음

### **2. 객체로 반환**

```jsx
// useEmailInput.js
export default function useEmailInput() {
  const [id, setId] = useInput("");
  const idRef = useRef(null);
  const [domain, setDomain] = useState("naver.com");

  return {
    id,
    idRef,
    onChangeEmail,
    domain,
    setDomain,
    onChangeDomain,
  };
}

// 사용
const { id, idRef, onChangeEmail } = useEmailInput();
```

- 어떤 값이 어떤 역할인지 **명확하게 알 수 있음**
- 필요한 값만 골라 구조분해 가능 → 확장성과 유지보수에 좋음

---

## **✅ 한 줄 요약**

> 상태는 부모에서 선언하고 자식은 props로 공유하며,

> 훅은 최상단에서만 호출하고, 커스텀 훅은 공통 로직을 깔끔하게 분리하는 도구!
