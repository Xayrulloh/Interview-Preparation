# Unit Testing Interview Questions

1. ## **What is Unit Testing?**

   _Unit testing means testing the **smallest independent piece of code**
   (usually a function or class method) to ensure it behaves correctly._

   ```ts
   function sum(a: number, b: number) {
     return a + b
   }

   test('adds 2 + 3 = 5', () => {
     expect(sum(2, 3)).toBe(5)
   })
   ```

2. ## **Why do we write Unit Tests?**

   - To catch bugs early.
   - To make refactoring safer.
   - To improve code quality and confidence before deploying.
   - To document intended behavior of code.

3. ## **What are mocks, stubs, and spies?**

   - **Mock:** Fake object/function to simulate real behavior.
   - **Stub:** Provides predefined responses.
   - **Spy:** Records how a function was used (calls, arguments).

   ```ts
   const sendEmail = jest.fn() // mock

   sendEmail('hello')
   expect(sendEmail).toHaveBeenCalledWith('hello') // spy
   ```

4. ## **How to test React components?**

   _Use React Testing Library + Jest_

   ```ts
   import { render, screen } from '@testing-library/react'
   import Button from './Button'

   test('renders button with text', () => {
     render(<Button label="Click Me" />)
     expect(screen.getByText('Click Me')).toBeInTheDocument()
   })
   ```

5. ## **What is Test-Driven Development (TDD)?**

   - Write tests **before** writing the actual implementation.
   - Cycle: **Red → Green → Refactor**.

6. ## **How do you handle external dependencies (like DB, API) in unit tests?**

   _Use **mocks** to avoid hitting real services._

   ```ts
   jest.mock('./api')

   import { getUser } from './api'

   test('should mock API call', async () => {
     ;(getUser as jest.Mock).mockResolvedValue({ id: 1, name: 'John' })
     const user = await getUser(1)
     expect(user.name).toBe('John')
   })
   ```

7. ## **What are common best practices in Unit Testing?**

   - Keep tests **fast**.
   - Test **behavior**, not implementation.
   - Use **clear naming** (`should do X when Y`).
   - Don’t over-mock → balance realism.
   - Aim for **80%+ coverage**, but focus on critical paths.

8. ## **How do you test asynchronous code?**

   _Use `async/await` or Jest’s `done` callback._

   ```ts
   async function fetchData() {
     return 'data'
   }

   test('fetchData returns data', async () => {
     const result = await fetchData()
     expect(result).toBe('data')
   })
   ```

9. ## **What is code coverage?**

   - Metric showing how much of the code is executed during tests.
   - Tools: Jest’s `--coverage` flag.
   - Types: Function coverage, branch coverage, line coverage.

10. ## **How do you test error handling?**

    _Use `try/catch` or Jest’s `rejects` matcher._

    ```ts
    async function fetchData() {
      return 'data'
    }

    test('fetchData throws error', async () => {
      await expect(fetchData()).rejects.toThrow()
    })
    ```
