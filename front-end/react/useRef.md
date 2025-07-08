# useRef는 언제, 왜 쓸까?

#### **✅ 1. DOM 직접 접근할 때 (ex. 포커스 주기)**

- input에 커서 자동으로 주고 싶을 때 등

```javascript
const inputRef = useRef(null);

useEffect(() => {
  inputRef.current?.focus();
}, []);

<input ref={inputRef} />;
```

#### **✅ 2. 값 저장소처럼 쓸 때 (렌더링 없이 값 보존)**

- 렌더링 없이 어떤 값을 기억하고 싶을 때
- 예: 이전 값 저장, setTimeout ID 저장, 외부 라이브러리 인스턴스 저장 등

```javascript
const timerRef = useRef(null); // setTimeout ID 저장
timerRef.current = setTimeout(...);
```

#### **✅ 특징 정리**

- ref는 화면에 영향을 주지 않는 **"참조값 저장소"** 일 뿐이라, .current에 값이 저장됨 (current는 바뀌어도 렌더링 X)
- 컴포넌트가 리렌더링돼도 값이 유지됨
- 상태처럼 화면을 바꾸는 게 목적이 아니고, 단순히 **참조값 저장**할 때 사용
- DOM 접근이 필요할 땐 document.getElementById() 대신 ref 사용하기!

---

> [!NOTE] 왜 React에서 DOM 직접 조작을 지양할까?

#### **✅ 1. React는 Virtual DOM 기반**

- React는 **상태(state)** 변화에 따라 Virtual DOM을 업데이트하고,
  실제 DOM과 비교(diff)해서 필요한 부분만 바꿔줌
- 직접 DOM 조작하면 React가 그걸 모름 → **불일치 발생**

#### **✅ 2. 상태와 UI가 분리되면 버그 발생**

- 예: document.getElementById().textContent = "" 같이 DOM을 바꾸면
  → 상태는 그대로인데 화면만 바뀜
  → React가 다시 렌더링하면 원래대로 덮어씌워버림

#### **✅ 3. 코드가 예측 불가능해지고 유지보수 어려움**

- 특정 DOM 조작 로직이 숨어 있으면 컴포넌트 재사용, 디버깅이 어려움
- 반면 useState 기반으로 UI를 관리하면 언제, 왜 화면이 바뀌는지 명확함

#### **✅ 4. React 철학에 어긋남**

- React의 기본 철학: **“UI는 상태의 함수”**
- 직접 DOM을 바꾸면 이 흐름을 깨트리게 됨

---

### **✅ 그래서 어떻게 해야 할까?**

- DOM 조작이 필요하면 useRef 사용
- UI 내용은 상태(useState)로 관리해서 React가 화면을 알아서 업데이트하도록 맡기기
