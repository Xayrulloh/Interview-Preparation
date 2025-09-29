# Effector State Management Interview Questions

1. ## **What is Effector?**

   _Effector is a **reactive state manager** for JavaScript apps. Unlike Redux
   or Zustand, it focuses on **event-driven updates** and **predictable state
   changes** with strong TypeScript support._

2. ## **What are the core concepts in Effector?**

   - **Event:** A function that describes an action (e.g., button click).
   - **Store:** Holds state and reacts to events.
   - **Effect:** Handles async logic (API calls, side effects).
   - **Domain:** Groups related events, stores, and effects.

   ```ts
   import { createEvent, createStore } from 'effector'

   // Event
   const increment = createEvent()

   // Store
   const $counter = createStore(0).on(increment, state => state + 1)

   // Usage
   increment()

   console.log($counter.getState()) // 1
   ```

3. ## **What is the difference between Event and Effect?**

   - **Event:** Describes **synchronous** actions (e.g., increment a counter).
   - **Effect:** For **async** logic (e.g., fetching users from API).

   ```ts
   import { createEffect } from 'effector'

   const fetchUserFx = createEffect(async (id: number) => {
     const res = await fetch(`/api/users/${id}`)

     return res.json()
   })

   fetchUserFx(1).then(user => console.log(user))
   ```

4. ## **How does Effector differ from Redux?**

   - Effector has **no reducers** – it uses `.on()` directly on stores.
   - It’s **more declarative** and **less boilerplate**.
   - Built-in async handling via `createEffect`.
   - Works **better with TypeScript** (inferred types).

5. ## **What is a Domain in Effector?**

   _A **Domain** groups related stores, events, and effects into one namespace.
   Useful for large apps._

   ```ts
   import { createDomain } from 'effector'

   const userDomain = createDomain()

   const fetchUserFx = userDomain.createEffect(async (id: number) => {
     const res = await fetch(`/api/users/${id}`)

     return res.json()
   })

   const userLoaded = userDomain.createEvent()
   const $user = userDomain
     .createStore(null)
     .on(fetchUserFx.doneData, (_, user) => user)
   ```

6. ## **How do you combine multiple stores in Effector?**

   _Using `combine()`._

   ```ts
   import { createStore, combine } from 'effector'

   const $firstName = createStore('John')
   const $lastName = createStore('Doe')

   const $fullName = combine(
     $firstName,
     $lastName,
     (first, last) => `${first} ${last}`
   )

   console.log($fullName.getState()) // John Doe
   ```

7. ## **How do you test Effector logic?**

   _Effector is very test-friendly because stores are just **pure functions**._

   ```ts
   test('counter increments', () => {
     const increment = createEvent()
     const $counter = createStore(0).on(increment, s => s + 1)

     increment()

     expect($counter.getState()).toBe(1)
   })
   ```

8. ## **What is the role of sample in Effector?**

   `_sample` connects **events/effects/stores** together. It’s used for advanced
   control flows.\_

   ```ts
   import { createEvent, createStore, sample } from 'effector'

   const loginClicked = createEvent()
   const $username = createStore('john')

   sample({
     source: $username,
     clock: loginClicked,
     fn: username => ({ username, password: '1234' }),
     target: console.log
   })

   loginClicked()
   // { username: "john", password: "1234" }
   ```

<br>

# 📊 Zustand vs Effector Comparison

| Feature            | **Zustand** 🐻                                        | **Effector** ⚡                            |
| ------------------ | ----------------------------------------------------- | ------------------------------------------ |
| **Core Concept**   | Store + Hooks                                         | Events + Stores + Effects                  |
| **Boilerplate**    | Very minimal                                          | Slightly more setup (events/effects)       |
| **Async handling** | Handled manually (with middleware or async functions) | Built-in with `createEffect`               |
| **TypeScript**     | Good (with generics)                                  | Excellent (auto-inference)                 |
| **Reactivity**     | Pull-based (use hook in component)                    | Push-based (event-driven)                  |
| **Learning Curve** | Easy                                                  | Medium                                     |
| **Ecosystem**      | Small, minimal                                        | Larger, supports complex apps              |
| **Best for**       | Small/medium apps needing simplicity                  | Medium/large apps with complex state flows |
