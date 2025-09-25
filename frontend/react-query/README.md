# React Query Interview Questions

1.  ## **What is React Query and why use it?**

    _React Query is a data-fetching and caching library for React_

    - Manages **server state** (data from APIs, databases, etc.).
    - Handles caching, background refetching, synchronization, and stale data.
    - Removes the need for manual `useEffect` + `useState` for fetching

    ```tsx
    import { useQuery } from '@tanstack/react-query'

    function Users() {
      const { data, isLoading, error } = useQuery({
        queryKey: ['users'],
        queryFn: () => fetch('/api/users').then(res => res.json())
      })

      if (isLoading) return <p>Loading...</p>
      if (error) return <p>Error fetching users</p>

      return (
        <ul>
          {data.map(u => (
            <li key={u.id}>{u.name}</li>
          ))}
        </ul>
      )
    }
    ```

2.  ## **What’s the difference between React Query and Redux/Zustand?**

    _👉 Best practice: Use React Query for server state + Zustand/Redux for
    client state_

    - **Redux/Zustand:** Manage **client state** (UI state, toggles, form
      inputs).
    - **React Query:** Manage **server state** (API data, caching, background
      refetching)

3.  ## **What is a `queryKey` in React Query?**

    - A unique **identifier for a query**.
    - React Query uses it for caching and invalidation.

    ```tsx
    useQuery({
      queryKey: ['todos', userId], // unique per user
      queryFn: () => fetch(`/api/todos?user=${userId}`).then(res => res.json())
    })
    ```

4.  ## **What is the difference between `useQuery` and `useMutation`?**

    - `useQuery`: Fetch **read-only data** (GET).
    - `useMutation`: Perform **write operations** (POST, PUT, DELETE).

    ```tsx
    import { useMutation, useQueryClient } from '@tanstack/react-query'

    function AddTodo() {
      const queryClient = useQueryClient()
      const mutation = useMutation({
        mutationFn: newTodo =>
          fetch('/api/todos', {
            method: 'POST',
            body: JSON.stringify(newTodo)
          }),
        onSuccess: () => {
          queryClient.invalidateQueries(['todos']) // refetch after adding
        }
      })

      return (
        <button onClick={() => mutation.mutate({ title: 'Learn React Query' })}>
          Add Todo
        </button>
      )
    }
    ```

5.  ## **What is Stale-While-Revalidate in React Query?**

    _React Query marks data as:_

    - **Fresh:** just fetched, won’t refetch.
    - **Stale:** older, may trigger background refetch.
    - **Inactive:** not used by any component.
    - **Garbage Collected:** removed after some time.

    _👉 This gives fast UI (cached data) + fresh updates (background refetch)._

6.  ## **How do you refetch data manually in React Query?**

    ```tsx
    const { refetch } = useQuery({
      queryKey: ['user', id],
      queryFn: () => fetch(`/api/user/${id}`).then(res => res.json())
    })

    // Button to manually refetch
    ;<button onClick={() => refetch()}>Refresh</button>
    ```

7.  ## **How do you invalidate queries in React Query? Why?**

    - Invalidation tells React Query: “This data is outdated, refetch it.”
    - Useful after mutations.

    ```tsx
    const queryClient = useQueryClient()
    queryClient.invalidateQueries(['todos'])
    ```

8.  ## **What is the difference between enabled and refetchOnWindowFocus?**

    - **`enabled: false`:** prevents query from running until you trigger it
      manually.
    - **`refetchOnWindowFocus: true`:** automatically refetches when user
      returns to the tab.

    ```tsx
    useQuery({
      queryKey: ['profile'],
      queryFn: fetchProfile,
      enabled: !!userId, // run only if userId exists
      refetchOnWindowFocus: true
    })
    ```

9.  ## **How does React Query handle caching?**

    - Stores API responses in cache, keyed by `queryKey`.
    - When a component mounts, it checks cache first before refetching.
    - Expired (stale) data may still be shown until new data arrives.

10. ## **How do you persist React Query cache (e.g., to localStorage)?**

    ```tsx
    import { persistQueryClient } from '@tanstack/react-query-persist-client'
    import { createSyncStoragePersister } from '@tanstack/query-sync-storage-persister'

    const persister = createSyncStoragePersister({
      storage: window.localStorage
    })

    persistQueryClient({
      queryClient,
      persister
    })
    ```

11. ## **What are some React Query performance optimizations?**

    - Use **selectors** to pick only needed parts of data.
    - Use `staleTime` to avoid unnecessary refetches.
    - Use `enabled` to conditionally fetch.
    - Use pagination (`useInfiniteQuery`) for large lists.

12. ## **When should you NOT use React Query?**

    - For **pure client-side state** (form inputs, UI toggles, modals).
    - If data doesn’t come from a server (use Zustand/Redux/Context instead).

13. ## **What is useInfiniteQuery in React Query?**

    _Used for **paginated data fetching** (e.g., infinite scroll)._

    ```tsx
    const { data, fetchNextPage, hasNextPage } = useInfiniteQuery({
      queryKey: ['posts'],
      queryFn: ({ pageParam = 1 }) =>
        fetch(`/api/posts?page=${pageParam}`).then(res => res.json()),
      getNextPageParam: (lastPage, allPages) => lastPage.nextPage ?? undefined
    })
    ```

14. ## **How does React Query help with optimistic updates?**

    - Update UI immediately before the server responds.
    - If server fails → rollback changes.

    ```tsx
    const mutation = useMutation({
      mutationFn: updateTodo,
      onMutate: async newTodo => {
        await queryClient.cancelQueries(['todos'])
        const prevTodos = queryClient.getQueryData(['todos'])
        queryClient.setQueryData(['todos'], old =>
          old.map(t => (t.id === newTodo.id ? { ...t, ...newTodo } : t))
        )
        return { prevTodos } // rollback point
      },
      onError: (err, newTodo, context) => {
        queryClient.setQueryData(['todos'], context.prevTodos)
      },
      onSettled: () => {
        queryClient.invalidateQueries(['todos'])
      }
    })
    ```

15. ## **How does React Query improve DX (developer experience)?**

    - Removes boilerplate (no reducers, no action types like Redux).
    - Provides caching, retries, refetching out-of-the-box.
    - Built-in DevTools for debugging queries.

<br>

# ⚖️ React Query vs RTK (React Toolkit) Query

| Feature / Aspect   | **React Query** ⚡                                                                  | **RTK Query (Redux Toolkit Query)** 🔥                                                              |
| ------------------ | ----------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| **Purpose**        | Library for **server-state management** (fetching, caching, syncing).               | A data-fetching & caching tool **built into Redux Toolkit**.                                        |
| **State Type**     | Manages only **server state** (data from API).                                      | Manages **server state** but also ties into **Redux global store** (can combine with client state). |
| **Setup**          | Install `react-query`, wrap app in `QueryClientProvider`.                           | Comes with Redux Toolkit; requires Redux store setup.                                               |
| **Boilerplate**    | Very low – just `useQuery`, `useMutation`.                                          | More boilerplate since it’s tied to Redux store, slices, API service definitions.                   |
| **API Definition** | No API slice, just define query functions directly.                                 | Define an `apiSlice` with `createApi` & endpoints.                                                  |
| **Learning Curve** | Easy to start, quick to use.                                                        | Steeper, since you need Redux concepts (slices, store, middleware).                                 |
| **Caching**        | Advanced caching: background refetch, stale-time, cache-time, invalidation.         | Caching + auto invalidation based on tags.                                                          |
| **Persistence**    | Needs extra setup (`react-query-persist-client`).                                   | Can integrate persistence via Redux Persist.                                                        |
| **DevTools**       | Excellent devtools (visualize queries, cache, status).                              | Uses Redux DevTools + RTK Query middleware logs.                                                    |
| **Async Handling** | Automatic loading, error, retry states.                                             | Automatic, but tied into Redux store updates.                                                       |
| **When to Use?**   | Best for apps that need **quick API fetching, caching, and syncing** without Redux. | Best for apps already using **Redux for client state**, and you want API state in the same store.   |
