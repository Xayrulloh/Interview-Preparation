# E2E Testing Interview Questions

1. ## **What is E2E Testing?**

   _E2E testing verifies that the **entire application flow** works as expected,
   from UI → API → DB → external services._

2. ## **Which tools are used for E2E testing?**

   - **Backend (API-based):**
     - Jest + Supertest
     - Pact (for contract testing)
   - **Frontend (UI-based):**
     - Cypress
     - Playwright
     - Selenium

3. ## **Example of E2E Test in Cypress (Frontend + API)**

   ```js
   describe('User Signup Flow', () => {
     it('should register, login, and view profile', () => {
       cy.visit('/register')
       cy.get('input[name="email"]').type('john@example.com')
       cy.get('input[name="password"]').type('123456')
       cy.get('button[type="submit"]').click()

       cy.url().should('include', '/login')

       cy.get('input[name="email"]').type('john@example.com')
       cy.get('input[name="password"]').type('123456')
       cy.get('button[type="submit"]').click()

       cy.url().should('include', '/dashboard')
       cy.contains('john@example.com')
     })
   })
   ```

4. ## **How do you handle database state in E2E tests?**

   - Use a **separate test DB**.
   - Reset DB before each test (`truncate` or use migrations).
   - Use **Testcontainers** for ephemeral DBs in CI.

5. ## **How do you test external APIs in E2E?**

   - Mock APIs (using MSW / Nock).
   - Use staging environments for external services.
   - Contract testing (e.g., Pact).

6. ## **How do you test authentication flows in E2E?**

   - Register/login → extract JWT → use in next requests.
   - Or pre-seed test DB with a known user and token.

7. ## **What are common challenges in E2E Testing?**

   - Slower than unit/integration tests.
   - Flaky tests due to timing/network issues.
   - Test data management.
   - CI/CD setup (test DB, containers, headless browsers).

8. ## **Best Practices for E2E Testing**

   - Keep E2E tests **minimal but critical** (auth, checkout, payments).
   - Use **realistic data** (not just mocks).
   - Run E2E in **CI/CD pipeline** with clean environment.
   - Prefer **headless browsers** (Playwright, Cypress in CI).
   - Separate test stages: unit → integration → e2e.

9. ## **Do you write more unit or E2E tests?**

   _“I write unit tests for logic-heavy code, integration tests for
   service-to-service interactions, and E2E tests for critical business flows
   like authentication and payments. I balance speed and coverage.”_
