# <center>YAGNI</center>

**YAGNI** stands for **You Aren't Gonna Need It**. It is a software development
principle that states:

> **"Don't implement something until it is necessary."**

_The idea is to avoid adding **features**, **abstractions**, or logic that might
be needed in the **future** but are not required **right now**. By following
YAGNI, developers keep the codebase **clean**, **simple**, and **easier to
maintain**._

---

- ## **Core Idea:**

  - Build only what you need **today**.
  - Avoid **over engineering** or preparing for **hypothetical** future cases.
  - Helps reduce **unnecessary complexity**, **cost**, and **bugs**.

---

- ## **Bad Example (violating YAGNI):**

  ```ts
  // Building for future: user might want multiple addresses (not needed now)
  class UserProfile {
    private addresses: string[]

    constructor(primaryAddress: string) {
      this.addresses = [primaryAddress]
    }

    addAddress(address: string) {
      this.addresses.push(address)
    }

    getAddresses(): string[] {
      return this.addresses
    }
  }

  // Current requirement: we only need ONE address per user.
  const user = new UserProfile('123 Main St')

  console.log(user.getAddresses()) // Overengineered
  ```

---

- ## **Good Example (applying YAGNI):**

  ```ts
  // Keep it simple: only one address per user as required
  class UserProfile {
    constructor(private address: string) {}

    getAddress(): string {
      return this.address
    }
  }

  const user = new UserProfile('123 Main St')
  console.log(user.getAddress()) // ✅ Simple and meets requirements
  ```

---

- ## **Real-World Example (NestJS Service):**

  **Without YAGNI (over engineering):**

  ```ts
  @Injectable()
  export class UserService {
    private users: User[] = []

    // Adding caching and complex filters (not required yet)
    private cache = new Map<string, User>()

    createUser(user: User) {
      this.users.push(user)
      this.cache.set(user.id, user)
    }

    getUser(id: string) {
      return this.cache.get(id) // Premature optimization
    }

    getUsersWithFilter(filter: GetUserFilter) {
      // Overcomplicated filter logic (not requested)
      return this.users.filter(u => u.role === filter.role)
    }
  }
  ```

  ✅ **With YAGNI (just enough to solve the problem):**

  ```ts
  @Injectable()
  export class UserService {
    private users: User[] = []

    createUser(user: User) {
      this.users.push(user)
    }

    getUser(id: string) {
      return this.users.find(u => u.id === id)
    }
  }
  ```

---

- ## **Benefits of YAGNI:**

  - **Reduces** unnecessary **complexity**.
  - Keeps code **focused on current needs**.
  - **Prevents wasted development effort**.
  - Makes future **refactoring easier**.

---

_🚀 **Summary:** **YAGNI** reminds us that writing code **"just in case"** often
leads to more harm than good. Build **only what you need now**, and evolve the
system as real requirements emerge._
