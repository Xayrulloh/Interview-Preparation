# <center>DRY (Don’t Repeat Yourself)</center>

_The DRY principle is a software development practice that states: <br> “Every
piece of knowledge must have a single, unambiguous, authoritative representation
within a system.”_

- **In short:** _avoid duplication._
- Instead, abstract repeated logic into **reusable** components, functions, or
  modules.
- If you find yourself **copy-pasting code** → probably a violation of DRY.

---

- ## Bad Example (Violation of DRY)

  ```ts
  // Duplicate logic for calculating discounts

  function getBookPrice(price: number, discount: number): number {
    return price - price * discount
  }

  function getElectronicsPrice(price: number, discount: number): number {
    return price - price * discount
  }

  function getClothesPrice(price: number, discount: number): number {
    return price - price * discount
  }

  console.log(getBookPrice(100, 0.1)) // 90
  console.log(getElectronicsPrice(200, 0.2)) // 160
  console.log(getClothesPrice(50, 0.15)) // 42.5
  ```

  **Problem:**

  - Same logic **repeated** in three different functions.
  - **Hard to maintain:** if discount formula changes, you must update
    everywhere.

---

- ## Good Example (Implementation of DRY)

  ```ts
  // Single reusable function

  function getDiscountedPrice(price: number, discount: number): number {
    return price - price * discount
  }

  console.log(getDiscountedPrice(100, 0.1)) // 90
  console.log(getDiscountedPrice(200, 0.2)) // 160
  console.log(getDiscountedPrice(50, 0.15)) // 42.5
  ```

  **Benefits:**

  - **One source of truth:** discount calculation logic is in a single place.
  - **Easier maintenance:** change once, applies everywhere.

---

- ## Real World Example (NestJs Service Layer)

  ```ts
  // ❌ Bad: repeating DB query logic in multiple controllers

  // user.controller.ts
  @Get(':id')
  async getUser(@Param('id') id: string) {
    return this.prisma.user.findUnique({ where: { id } })
  }

  // order.controller.ts
  @Get(':userId/orders')
  async getOrders(@Param('userId') userId: string) {
    const user = await this.prisma.user.findUnique({ where: { id: userId } })
    if (!user) throw new NotFoundException('User not found')
    return this.prisma.order.findMany({ where: { userId } })
  }
  ```

  ```ts
  // ✅ Good: reuse logic in a service (DRY)

  // user.service.ts
  @Injectable()
  export class UserService {
    constructor(private prisma: PrismaService) {}

    async findById(id: string) {
      return this.prisma.user.findUnique({ where: { id } })
    }
  }

  // order.controller.ts
  @Get(':userId/orders')
  async getOrders(@Param('userId') userId: string) {
    const user = await this.userService.findById(userId)
    if (!user) throw new NotFoundException('User not found')
    return this.prisma.order.findMany({ where: { userId } })
  }
  ```

---

- ## Key Takeaways:

  - **Avoid duplication** of logic, queries, or UI code.
  - **Centralize logic:** use helpers, services, or utilities.
  - DRY improves **maintainability** and reduces **bugs**.
  - But ⚠️ Don’t overdo it → sometimes too much abstraction can make code harder
    to read (`“WET – Write Everything Twice” may be fine for very small cases`).
