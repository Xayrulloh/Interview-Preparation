# React Interview Questions

1.  ## **What is React and how does it work**

    _React is an open-source JavaScript library for building user interfaces_

    - It’s based on components, which are reusable building blocks of UI.
    - React uses a Virtual DOM to efficiently update the real DOM.
    - When state changes, React creates a new virtual DOM, compares it with the
      old one (diffing algorithm), and applies only the necessary updates
      (reconciliation).

2.  ## **What is JSX and why is it used**

    _JSX is a JavaScript syntax extension that looks like HTML_

    - It makes UI code easier to write and understand.
    - JSX prevents injection attacks by escaping values before rendering.
    - Under the hood, JSX is compiled to React.createElement() calls.

3.  ## **What is a stateless component**

    - **Stateless component:**
      - Receives data via props.
      - Does not manage its own state.
      - Example:
        ```tsx
        const Button = ({ label }) => <button>{label}</button>
        ```
    - **Stateful component:**
      - Manages its own state.
      - Can respond to user interactions.
      - Example (using hooks):
      ```tsx
      const Counter = () => {
        const [count, setCount] = useState(0)
        return <button onClick={() => setCount(count + 1)}>{count}</button>
      }
      ```

4.  ## **What is the difference between state and props?**

    - **State:**

      - Internal to a component.
      - Mutable (updated with setState or hooks).

    - **Props:**

      - Passed from parent to child.
      - Immutable inside the child.

5.  ## **How do you update state in React?**

    - **Class components:** _this.setState({ key: value })_
    - **Function components:** _setState(newValue) via **useState**_

6.  ## **What is a Higher Order Component (HOC)?**

    _A function that takes a component and returns a new component with extra
    features_

    ```ts
    const withLogger = Component => props => {
      console.log('Props:', props)
      return <Component {...props} />
    }
    ```

7.  ## **What is React Context?**

    _Context provides a way to share values (like theme, auth user, or language)
    without passing props through multiple levels_

    - Created with React.createContext().
    - Consumed via useContext or <Context.Consumer>.

8.  ## **What is a React Hook?**

    _Hooks let functional components use features like state and lifecycle
    methods_

    - **useState**, **useEffect**, **useContext**, **useReducer**

9.  ## **Difference between useEffect and useLayoutEffect**

    - **useEffect:** _Runs asynchronously after render, good for side effects
      like data fetching._
    - **useLayoutEffect:** _Runs synchronously after DOM mutations but before
      the browser repaints — used for DOM measurements._

10. ## **List of Common React Hooks**

    - `useState`: _Manages local state in functional components._
    - `useEffect`: _Handles side effects such as data fetching or
      subscriptions._
    - `useContext`: _Accesses context values without prop drilling._
    - `useReducer`: _Manages complex state logic._
    - `useCallback`: _Memoizes callback functions._
    - `useMemo`: _Memoizes computed values._
    - `useRef`: _Accesses mutable values or DOM nodes._
    - `useLayoutEffect`: _Like `useEffect`, but fires synchronously after DOM
      mutations._
    - `useImperativeHandle`: _Customizes the instance value exposed to parent
      components when using `ref`._
    - `useDebugValue`: _Displays a label for custom hooks in React DevTools._
    - `useId`: _Generates unique IDs for accessibility attributes._

11. ## **Class Component vs Function Component**

    - **Class Component**: Uses ES6 classes, supports lifecycle methods, and
      manages state with `this.state` and `this.setState`.
    - **Function Component**: Uses plain functions, can use hooks for state and
      side effects, generally simpler and preferred in modern React.

12. ## **Component Lifecycle**

    - **Mounting**: `constructor`, `componentDidMount → useEffect(() => {}, [])`
    - **Updating**: `shouldComponentUpdate`, `componentDidUpdate → useEffect`
      with deps
    - **Unmounting**: `componentWillUnmount` → cleanup in `useEffect`

13. ## **What are React Keys and why are they important?**

    _Keys help React identify which list items `changed`, `added`, or
    `removed`._

    - Keys must be`unique`and`stable` (not array indexes if list can reorder).

14. ## **Controlled vs Uncontrolled Components**

    - **Controlled**: _Form input values controlled by React state
      (value={state} with onChange)._
    - **Uncontrolled**: _Form values handled by the DOM, accessed via ref._

15. ## **What are Error Boundaries?**

    _Special components that catch JavaScript errors in child components and
    show a fallback UI._

    - Implemented with `componentDidCatch` and `getDerivedStateFromError`.
    - Functional alternative: libraries like `react-error-boundary`.

16. ## **What is React Fiber?**

    _Fiber is React’s reconciliation engine (since React 16)._

    - Breaks rendering work into chunks.
    - Improves responsiveness by `pausing`, `aborting`, or `reusing` work.

17. ## **How do you optimize performance in React?**

    - Use `React.memo` for pure components.
    - Use `useMemo` and `useCallback` to memoize expensive
      calculations/functions.
    - `Lazy load` components with `React.lazy + Suspense`.
    - Avoid unnecessary re-renders (proper keys, split components).

18. ## **What is Server-Side Rendering (SSR) in React?**

    - `Rendering` React components on the `server` and sending `HTML` to the
      `client`.
    - Improves `SEO` and initial `load time`.
    - Frameworks: `Next.js, Remix`.

19. ## **What is React Query?**

    _A data-fetching library that handles:_

    - Caching
    - Background updates
    - Automatic refetching
    - Synchronizing server state

20. ## **What is React Suspense?**

    _A feature for handling asynchronous operations in components (e.g., data
    fetching, lazy loading)._

    - Works with `React.lazy` for code splitting.
    - Will integrate deeply with `React Server Components`.

21. ## **What are React Server Components (RSC)?**

    - Introduced in `React 18+`.
    - Components that render on the `server`, send serialized output to the
      `client`.
    - `Reduce` bundle size and `improve` performance.

22. ## **22. What are Portals in React?**

    _A way to render children into a DOM node outside the parent component’s
    hierarchy._

    ```tsx
    ReactDOM.createPortal(child, document.getElementById('modal-root'))
    ```

23. ## **What is Prop Drilling? How to avoid it?**

    _Prop drilling = passing props through many nested components._

    - Avoided by `Context API`, state managers (Redux, Zustand, Recoil), or
      composition patterns.

24. ## **What is Redux and when to use it?**

    _Redux is a predictable state container for JavaScript apps._

    - Best for large apps with `global shared state`.
    - Alternatives: `Zustand, Recoil, Jotai, MobX`.

25. ## **Virtual DOM**

    _The `Virtual DOM (VDOM)` is a lightweight JavaScript representation of the
    actual DOM._

    - When state changes, React builds a new virtual DOM tree.
    - It then compares it with the previous tree (`diffing`).
    - Only the changed parts are updated in the real DOM (`reconciliation`).

    This improves performance by reducing costly direct DOM manipulations.

26. ## **React Reconciliation**

    _Reconciliation is React’s process of updating the real DOM._

    - React compares the new virtual DOM with the old one (diffing).
    - Changes are applied selectively instead of re-rendering the entire UI.
    - Keys help React optimize reconciliation in lists.

27. ## **React Context**

    _React Context provides a way to share data across the component tree
    without passing props manually at every level._

    - Good for global values (theme, authentication, locale).
    - Works with `createContext`, `Provider`, and `useContext`.
    - Overuse can cause unnecessary re-renders — for complex state, prefer a
      dedicated state manager.

28. ## **Props Drilling**

    _Props drilling is when props are passed down through multiple nested
    components just to reach a deeply nested child._

    - This makes code harder to maintain and less flexible.

    - Solutions:

      - Context API for global data.
      - State managers like Redux or Zustand.
      - Component composition (lifting state or using render props).

29. ## **State Managers**

    _State managers help manage `global or complex state` in large React apps._

    - **Redux:** Predictable, strict, great for debugging with DevTools.
    - **MobX:** Reactive, less boilerplate, easier for beginners.
    - **Zustand:** Lightweight, minimal API, built on hooks.
    - **Recoil / Jotai:** Modern, flexible alternatives for granular state
      control.

    - Use them when:

      - Multiple components need to share/update the same state.
      - Context becomes too complex or leads to performance issues.

30. ## **useContext Hook**

    _The useContext hook lets a functional component consume values from a
    Context directly._

    ```ts
    const ThemeContext = React.createContext('light')

    function Button() {
      const theme = useContext(ThemeContext)
      return <button className={theme}>Click me</button>
    }
    ```

    - Eliminates the need for `<Context.Consumer>`.
    - Great for small-scale state sharing (theme, language, auth user).

31. ## **React Query**

    _React Query (now `TanStack Query`) is a library for managing server state._

    - Handles fetching, caching, synchronizing, and updating async data.

    - Features:

      - Background refetching.
      - Automatic cache invalidation.
      - Request deduplication.
      - Optimistic updates.

    - Great replacement for Redux/Context when the main challenge is
      `server-side data fetching` rather than client-side state.
