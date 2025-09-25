# 🧪 Unit vs Integration vs E2E Testing

| Aspect                 | **Unit Test**                                   | **Integration Test**                               | **End-to-End (E2E) Test**                                               |
| ---------------------- | ----------------------------------------------- | -------------------------------------------------- | ----------------------------------------------------------------------- |
| **Definition**         | Tests a single function/component in isolation. | Tests how multiple modules/services work together. | Tests the full application flow from UI → API → DB → external services. |
| **Scope**              | Smallest (1 function/class).                    | Medium (service + DB, API + service).              | Largest (entire system, real user scenarios).                           |
| **Dependencies**       | None (use mocks/stubs).                         | Some real dependencies (e.g., DB, service layer).  | All real dependencies (DB, API, frontend, 3rd-party APIs).              |
| **Speed**              | Fastest ⚡ (ms).                                | Medium ⏱️ (seconds).                               | Slowest 🐢 (seconds to minutes).                                        |
| **Reliability**        | Very reliable (less flaky).                     | Reliable if environment is stable.                 | Can be flaky due to network/async/browser.                              |
| **Tools**              | Jest, Mocha, Vitest.                            | Jest + Supertest, Testcontainers, MSW.             | Cypress, Playwright, Selenium, Supertest (API E2E).                     |
| **Example (NestJS)**   | Test `hashPassword()` function with mock.       | Test `UserService.createUser()` with DB.           | Test `/auth/register → login → profile` full flow.                      |
| **Example (Frontend)** | Test `Button` component renders correctly.      | Test `LoginForm` calls API and updates state.      | Test "User registers → logs in → sees dashboard".                       |
| **Test Data**          | Dummy data / mocks.                             | Real test DB with fixtures.                        | Real DB + realistic data.                                               |
| **Purpose**            | Validate correctness of smallest pieces.        | Validate integration of modules/services.          | Validate user-facing flows work end-to-end.                             |
| **Best For**           | Logic-heavy functions, algorithms.              | API routes, DB queries, service-to-service logic.  | Critical business flows (auth, checkout, payments).                     |

## **In short**

- **Unit:** Is it correct? (one piece of code)
- **Integration:** Do they work together?
- **E2E:** Does the user journey work.
