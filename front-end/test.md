# 테스트 코드

### **(1) Unit Test (단위 테스트)**

- 하나의 함수, 컴포넌트 같은 **작은 단위**가 올바르게 동작하는지 테스트
- Jest, Vitest 같은 테스트 프레임워크 사용
- 예제: 버튼을 클릭하면 `count` 값이 증가하는지 확인

```javascript
import { render, screen, fireEvent } from "@testing-library/react";
import Counter from "./Counter"; // 테스트할 컴포넌트
import "@testing-library/jest-dom";

test("버튼 클릭 시 카운트 증가", () => {
  render(<Counter />);
  const button = screen.getByRole("button", { name: /증가/i });
  fireEvent.click(button);
  expect(button).toHaveTextContent("1");
});
```

### **(2) Integration Test (통합 테스트)**

- 여러 개의 모듈이 서로 잘 동작하는지 확인
- API 요청 후 UI가 정상적으로 렌더링되는지 확인하는 경우가 많음

```javascript
import { render, screen, waitFor } from "@testing-library/react";
import UserList from "./UserList";
import { getUsers } from "./api";

jest.mock("./api"); // API 요청을 가짜(mock)로 만듦

test("API에서 유저 목록이 정상적으로 렌더링됨", async () => {
  getUsers.mockResolvedValue([{ id: 1, name: "Alice" }]);
  render(<UserList />);
  await waitFor(() => screen.getByText("Alice"));
});
```

### **(3) E2E Test (엔드 투 엔드 테스트)**

- 사용자 흐름(User Flow)를 점검하는 테스트
- Cypress, Playwright 같은 도구 사용
- 예제: 로그인 페이지에서 ID/PW 입력 후 로그인 버튼을 누르면 메인 페이지로 이동하는지 테스트

```javascript
describe("로그인 테스트", () => {
  it("로그인 성공 후 메인 페이지로 이동", () => {
    cy.visit("/login");
    cy.get("input[name='username']").type("testuser");
    cy.get("input[name='password']").type("password123");
    cy.get("button").contains("로그인").click();
    cy.url().should("include", "/home");
  });
});
```
