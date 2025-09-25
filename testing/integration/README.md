# Integration Testing Interview Questions

1. ## **What is Integration Testing?**

   _Testing how multiple modules/components of an application work together_

2. ## **How do you handle the database in Integration Tests?**

   - Use a real DB (Postgres, MySQL) → reset data before each test.
   - Use in-memory DB (like SQLite or MongoDB Memory Server).
   - Use Testcontainers (Docker-based temporary DB).

3. ## **How do you mock external APIs in Integration Tests?**

   _Use tools like **nock** or **msw (Mock Service Worker)**._

   ```ts
   import nock from 'nock'

   it('should fetch user from external API', async () => {
     nock('https://api.example.com')
       .get('/user/1')
       .reply(200, { id: 1, name: 'John' })

     const result = await myService.getUserFromApi(1)
     expect(result.name).toBe('John')
   })
   ```

4. ## **What tools are commonly used for Integration Testing in Node/NestJS?**

   - **Jest:** Test runner.
   - **Supertest:** HTTP request testing.
   - **Testcontainers:** Ephemeral databases.
   - **Nock / MSW:** Mock APIs.

5. ## **How do you test authentication in Integration Tests?**

   _Simulate login, get a JWT, and use it in requests._

   ```ts
   it('GET /profile → should return profile with valid token', async () => {
     const login = await request(app.getHttpServer())
       .post('/auth/login')
       .send({ email: 'test@example.com', password: '123456' })

     const token = login.body.access_token

     const res = await request(app.getHttpServer())
       .get('/profile')
       .set('Authorization', `Bearer ${token}`)

     expect(res.status).toBe(200)
     expect(res.body.email).toBe('test@example.com')
   })
   ```

6. ## **What are common challenges in Integration Testing?**

   - Slow execution (DB, network calls).
   - Flaky tests (when depending on external services).
   - Test data management (resetting DB).
   - Deciding **what to mock vs what to use real**.

7. ## **Best Practices for Integration Testing**

   - Keep DB clean → truncate or reset between tests.
   - Use **realistic test data**.
   - Test **happy path + edge cases**.
   - Run integration tests in **CI/CD pipeline**.
   - Don’t overdo → integration tests are slower than unit tests.

8. ## **Do you prefer unit tests or integration tests?**

   _“I use unit tests for core logic and integration tests for critical flows
   like authentication, database operations, and API calls. This balance ensures
   both speed and reliability.”_
