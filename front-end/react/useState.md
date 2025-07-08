# useState

1. setId(e.target.value)를 호출한 직후에 console.log("after", id)를 실행해도 여전히 이전 상태값("")이 출력됩니다.

2. 이는 React의 state 업데이트가 비동기적으로 처리되기 때문입니다. state 업데이트는 다음 렌더링 사이클에서 적용됩니다.

3. 실제로 새로운 값이 반영되는 시점은
   - 컴포넌트가 다시 렌더링될 때
   - 즉, App 컴포넌트가 다시 호출될 때

```javascript
function App() {
  const [현재상태, set상태] = useState(
    "초기 상태 | 아무것도 지정안하면 undefined"
  );
  // [] 배열에다 담아야함 {} 객체 X

  // 리액트는 항상 현재 상태를 바라보고, 상태가 바뀌면 다음번 앱을 호출 할 때 그 때 서야 접근 가능
  const domains = ["naver.com", "google.com", "kakao.com"];

  return (
    <>
      <div>
        <div>
          <input type="text" />

          {domain === "" ? null : <span>@</span>}

          <select>
            {domains.map((d) => {
              return (
                <option key={d} value={d}>
                  {d}
                </option>
              );
            })}

            <option value="">직접입력</option>
          </select>
        </div>

        <input type="password" />

        <button>로그인</button>
      </div>

      <div>회원가입</div>
    </>
  );
}
```
