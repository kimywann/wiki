# ✅ useEffect란?

**useEffect**는 “리액트 컴포넌트가 DOM에 영향을 미치는 작업”이나 “외부 시스템과 연결되는 작업”을 할 때 사용하는 **사이드 이펙트(side effect)** 전용 훅입니다.

### **📌 쉽게 말하면**

리액트는 기본적으로 “상태에 따라 화면을 그리는 일”에만 집중해요.
그런데 네트워크 요청, 브라우저 이벤트 등록, 콘솔 출력, 수동으로 DOM에 접근 등은 **리액트 밖의 세상과 연결된 일들**이잖아요? 그럴 때 useEffect를 씁니다.

---

## **🧠 구조 복습**

```jsx
useEffect(() => {
  // 실행할 작업

  return () => {
    // 컴포넌트가 unmount되거나 의존성 배열 값이 바뀌기 전에 실행됨 (clean-up)
  };
}, [의존성들]);
```

- []: 처음 마운트될 때만 실행
- [url]: url 값이 바뀔 때마다 실행
- 생략: 매 렌더링마다 실행 (거의 안 씀)

## **💡 사용 예시로 이해하기**

### **✅ 예시 1: 최초 마운트 시 이벤트 등록 (한 번만 실행)**

```jsx
useEffect(() => {
  window.addEventListener("popstate", () => {
    setUrl(window.location.pathname);
  });
}, []);
```

- ✅ [] 빈 배열 → **처음 렌더링 될 때만 실행됨**
- 이건 괜찮지만, 이벤트 리스너 등록할 때는 반드시 **클린업(clean-up)**을 해줘야 메모리 누수가 없어요.

---

### **⚠️ 예시 2: 잘못된 클린업 방식**

```jsx
useEffect(() => {
  window.addEventListener("popstate", onPopState);

  return () => {
    window.removeEventListener("popstate", () => {}); // ❌ 이건 제거 안됨!
  };
}, [url]);
```

- 여기서 실수는 **removeEventListener에 익명 함수를 넘긴 것**이에요.
- 이벤트 등록 시 넘긴 onPopState 함수와 **완전히 같은 함수**여야 제거가 됩니다.

👉 그래서 정확한 코드는 아래처럼 돼야 해요:

```jsx
useEffect(() => {
  const onPopState = () => {
    setUrl(window.location.pathname);
  };
  window.addEventListener("popstate", onPopState);

  return () => {
    window.removeEventListener("popstate", onPopState);
  };
}, []);
```

---

## **🎯 왜 의존성 배열이 중요할까?**

```jsx
useEffect(() => {
  console.log("run");
}, [url]);
```

- 위 코드는 url이 바뀔 때마다 다시 실행돼요.
- 그럼 내부에서 setUrl을 또 호출하면 다시 실행되고… → 무한루프 위험!
- 이럴 땐 의존성을 없애거나, 혹은 url이 바뀌는 걸 감지하는 게 맞는지 다시 생각해봐야 해요.

---

## **✅ 요약 정리**

| **개념**           | **설명**                                           |
| ------------------ | -------------------------------------------------- |
| useEffect의 역할   | 외부와의 연결 작업 (DOM, 이벤트, fetch, 타이머 등) |
| 의존성 배열 []     | 마운트될 때 딱 한 번 실행                          |
| 의존성 배열 [x]    | x가 바뀔 때마다 실행                               |
| 클린업 함수        | 메모리 누수 방지를 위한 정리 작업                  |
| DOM 접근           | 가능하면 리액트 방식(onClick 등)으로 처리          |
| 이벤트 리스너 등록 | 꼭 remove도 해줘야 함 (같은 함수로!)               |

---

## **🔍 부연 팁: useEffect 자주 안 써도 되는 경우**

- 버튼 클릭으로 라우팅할 거면:

```jsx
<a onClick={() => setUrl("/login")}>Login</a>
```

- 이런 식으로 처리하면 굳이 document.querySelector("a") 이런 건 안 써도 돼요.
- 그리고 React Router 쓰면 useEffect 없이도 라우팅 자동 처리됨
  (그래서 나중엔 useEffect를 쓸 일이 줄어들어요)
