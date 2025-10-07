# Zustand State Management Interview Questions

1. ## **What is Zustand and why use it instead of Redux?**

   - Zustand is a **lightweight state management** library for React.
   - It’s much simpler than Redux, with **minimal boilerplate** and **better
     DX**.
   - Unlike Redux, you don’t need actions, reducers, or middlewares.
   - State is just a **store function** + **hooks**.

   ```tsx
   import { create } from 'zustand'

   const useStore = create(set => ({
     count: 0,
     increase: () => set(state => ({ count: state.count + 1 }))
   }))

   function Counter() {
     const { count, increase } = useStore()
     return <button onClick={increase}>Count: {count}</button>
   }
   ```

2. ## **How does Zustand compare to Context API?**

   - **Context API:** Good for small apps, but can cause unnecessary re-renders.
   - **Zustand:** More efficient (only components using the state re-render),
     scalable, supports middleware, persistence, async logic.

3. ## **What are the key features of Zustand?**

   - Simplicity: no boilerplate.
   - Hooks-based API (`useStore`).
   - Selectors for performance optimization.
   - Supports async actions.
   - Middleware: persistence, devtools, immer, etc.

4. ## **How do you create a Zustand store?**

   ```tsx
   import { create } from 'zustand'

   // initialization
   const useAuthStore = create(set => ({
     user: null,
     login: userData => set({ user: userData }),
     logout: () => set({ user: null })
   }))

   // usage
   function Navbar() {
     const user = useAuthStore(state => state.user)
     return <div>{user ? `Welcome, ${user.name}` : 'Not logged in'}</div>
   }
   ```

5. ## **What are Selectors in Zustand and why use them?**

   - Selectors let you pick only the part of the state you need → reduces
     re-renders.

   ```tsx
   const count = useStore(state => state.count) // selector
   ```

6. ## **How does Zustand handle async actions?**

   - You can write async functions directly inside the store.

   ```tsx
   const useUserStore = create(set => ({
     user: null,
     fetchUser: async () => {
       const res = await fetch('/api/user')
       const data = await res.json()
       set({ user: data })
     }
   }))
   ```

7. ## **What is Zustand middleware?**

   _Zustand supports middleware for extra features:_

   - **Devtools:** Debugging like Redux DevTools.
   - **Persist:** Save state in localStorage.
   - **Immer:** Write mutable code.

   ```tsx
   // persist
   import { persist } from 'zustand/middleware'

   const useThemeStore = create(
     persist(
       set => ({
         theme: 'light',
         toggleTheme: () =>
           set(state => ({ theme: state.theme === 'light' ? 'dark' : 'light' }))
       }),
       { name: 'theme-storage' }
     )
   )
   ```

8. ## **How does Zustand avoid unnecessary re-renders?**

   - Zustand uses **selectors** and **shallow comparison** (shallow helper).
   - Components only re-render when the selected state changes.

   ```tsx
   import { shallow } from 'zustand/shallow'

   const { count, increase } = useStore(
     state => ({ count: state.count, increase: state.increase }),
     shallow
   )
   ```

9. ## **How do you share Zustand state across multiple components?**

   - The store is global by default.
   - You just call `useStore()` in any component.

10. ## **Can Zustand be used outside React components?**

    _Yes ✅ Unlike Context/Redux hooks, Zustand’s store can be used anywhere
    (e.g., API calls, services)._

    ```tsx
    const { increase } = useStore.getState()
    increase() // works outside React
    ```

11. ## **What are the main differences between Zustand and Redux Toolkit?**

    - **Redux Toolkit:** More structured, good for very large apps, has
      devtools, middleware, immer built-in.
    - **Zustand:** Minimal, flexible, no boilerplate, better DX, but fewer
      opinions.

12. ## **How do you reset Zustand state?**

    ```tsx
    const useStore = create(set => ({
      count: 0,
      reset: () => set({ count: 0 })
    }))

    // or the whole state
    useStore.setState({ count: 0 })
    ```

13. ## **Does Zustand support server-side rendering (SSR)?**

    - Yes ✅ Zustand works well with Next.js.
    - You can hydrate the store with initial state on the server.

14. ## **What are some performance optimizations in Zustand?**

    - Use selectors to read only needed state.
    - Use `shallow` comparison to prevent unnecessary renders.
    - Split stores by domain (authStore, cartStore, etc.).

15. ## **When should you choose Zustand over Redux?**

    - Small/medium apps → Zustand is easier & faster.
    - Large apps with complex async flows → Redux Toolkit may be better.
    - Zustand is preferred when you want simplicity, less boilerplate, and
      hooks-first API.
