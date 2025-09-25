# <center>KISS (Keep It Simple, Stupid)</center>

_The **KISS principle** is a design rule that emphasizes simplicity in software
systems. The idea is that most systems work best if they are kept simple rather
than made complex. Simplicity improves readability, maintainability, and reduces
bugs._

**Core idea:** Don’t over-engineer. Prefer simple, straightforward solutions
over unnecessarily complex abstractions.

---

- ## **Bad Example (Violation of KISS):**

  ```ts
  // Over-engineered multiplication function

  class MathOperation<T extends number> {
    constructor(private value: T) {}

    multiply<U extends number>(factor: U): number {
      return this.value * factor
    }
  }

  const result = new MathOperation(5).multiply(10)
  console.log(result) // 50
  ```

  **Problem:**

  - **Too abstract** for a simple multiplication.
  - **Harder** to read and maintain.
  - Adds **unnecessary boilerplate**.

---

- ## **Good Example (Apply KISS):**

  ```ts
  // Simple multiplication function

  function multiply(a: number, b: number): number {
    return a * b
  }

  console.log(multiply(5, 10)) // 50
  ```

  **Benefits:**

  - **Short**, **clear**, and **maintainable**.
  - **Anyone can understand** the purpose immediately.

---

- ## **Real-world Example (NestJS Controller):**

  ```ts
  // ❌ Bad: Over-engineered NestJS route

  @Get('users/:id')
  async getUser(
    @Param('id') id: string,
    @Res() res: Response,
    @Inject(forwardRef(() => UserService)) private readonly userService: UserService
  ) {
    const user = await this.userService.findById(id)

    if (!user) {
      return res.status(HttpStatus.NOT_FOUND).json({ message: 'User not found' })
    }

    return res.status(HttpStatus.OK).json(user)
  }
  ```

  ```ts
  // ✅ Good: Keep it simple

  @Get('users/:id')
  async getUser(@Param('id') id: string) {
    const user = await this.userService.findById(id)

    if (!user) throw new NotFoundException('User not found')

    return user
  }
  ```

---

- ## **Key Takeaways:**
  - Prefer **clarity** over cleverness.
  - **Don’t add complexity** unless it’s absolutely necessary.
  - **Simple code** is easier to test, debug, and maintain.
