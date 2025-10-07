# Next.js Interview Questions

1. ## **What is Next.js? Why use it?**

   - Next.js is a `React framework` for building server-rendered and statically
     generated applications.
   - Provides features like SSR, SSG, API routes, file-based routing, and image
     optimization.
   - Benefits: SEO-friendly, fast performance, developer experience, hybrid
     rendering.

2. ## **Difference between Next.js and React?**

   - **React**: UI library, focuses on building components.
   - **Next.js**: Framework built on React with SSR, SSG, routing, API, and
     optimizations out of the box.

3. ## **How does file-based routing work in Next.js?**

   - Pages inside the `pages/` (Next 12) or `app/` (Next 13+) directory become
     routes automatically.
   - Example: `pages/about.js` → `/about`.
   - Dynamic routes use `[param].js` → `/blog/[id]`.

4. ## **What are dynamic routes in Next.js?**

   - Routes defined using square brackets.
   - Example: `pages/blog/[id].js` matches `/blog/1`, `/blog/2`.
   - Use `getStaticPaths` for SSG or `getServerSideProps` for SSR with dynamic
     data.

5. ## **What is pre-rendering in Next.js?**

   _Next.js pre-renders pages by default for performance and SEO_

   **Two types:**

   - Static Generation (`SSG`): Builds HTML at build time.
   - Server-Side Rendering (`SSR`): Builds HTML on each request.

6. ## **What is the difference between SSR, SSG, and ISR?**

   - **SSR**: Page rendered on each request (`getServerSideProps`).
   - **SSG**: Page rendered at build time (`getStaticProps`).
   - **ISR (Incremental Static Regeneration)**: Static pages `revalidated` after
     `a given time`.

7. ## **What is getStaticProps in Next.js?**

   - Used for `SSG`.
   - Fetches data at build time.
   - Runs only on the server (never shipped to client).

8. ## **What is getServerSideProps?**

   - Used for `SSR`.
   - Runs at request time on the server.
   - Useful when data changes frequently or depends on request.

9. ## **What is getStaticPaths?**

   - Used with `getStaticProps` for `dynamic SSG`.
   - Defines which paths should be pre-rendered at build time.
   - Example: building static blog pages for each post.

10. ## **What is Incremental Static Regeneration (ISR)?**

    - Lets you update static pages after deployment.
    - Use `revalidate` inside `getStaticProps`.
    - Example: `revalidate: 60` regenerates the page every 60 seconds.

11. ## **What are API Routes in Next.js?**

    - Define backend endpoints inside `pages/api/`.
    - Example: `pages/api/users.js` → `/api/users`.
    - Used for server-side logic like auth, DB queries, etc.

12. ## **Difference between `Link` and `<a>` in Next.js?**

    - `next/link` enables **client-side navigation** (no full reload).
    - `<a>` causes a full page reload.

13. ## **What is Next.js Image Optimization?**

    - The `next/image` component optimizes images automatically.
    - Features: `lazy loading`, `resizing`, `WebP conversion`,
      `responsive images`.

14. ## **What is Middleware in Next.js?**

    - Middleware runs `before a request is completed`.
    - Use for `auth`, `redirects`, `logging`, `A/B testing`.
    - Example: `middleware.ts` in project root.

15. ## **What is the App Router in Next.js 13+?**

    - Introduced with `React Server Components`.
    - Uses `app/` directory instead of `pages/`.
    - Features: `Layouts`, `streaming`, `server components` by default.

16. ## **Difference between Pages Router and App Router?**

    - **Pages Router (<= Next 12)**: Uses `pages/`, `getStaticProps`,
      `getServerSideProps`.
    - **App Router (Next 13+)**: Uses `app/`, React Server Components, async
      components, `fetch` with caching.

17. ## **What are Layouts in Next.js App Router?**

    - Shared UI across multiple pages.
    - Defined with `layout.js` in `app/`.
    - Useful for navbars, footers, sidebars.

18. ## **How does Next.js handle SEO?**

    - Pre-rendering improves SEO.
    - `next/head` allows custom meta tags.
    - App Router: `metadata` API for SEO settings.

19. ## **How to add metadata in Next.js 13+?**

    - Use the new `export const metadata` API inside page or layout.

    ```ts
    export const metadata = {
      title: 'Home Page',
      description: 'Welcome to my app'
    }
    ```

20. ## **What is Static Export in Next.js?**

    - Export app as a static site using `next export`.
    - Removes need for a Node.js server.
    - Works best for purely static content.

21. ## **What is React Server Component (RSC) in Next.js?**

    - Runs only on the server, never in the client bundle.
    - Reduces bundle size and improves performance.
    - Default in `app/` router.

22. ## **How does caching work in Next.js 13 fetch API?**

    - `fetch` supports built-in caching strategies:
      - `cache: 'force-cache'` (default, SSG).
      - `cache: 'no-store'` (always fetch fresh, SSR).
      - `revalidate: <seconds>` (ISR).

23. ## **How do you handle environment variables in Next.js?**

    - Store in `.env.local`.
    - Access via `process.env.KEY`.
    - Prefix with `NEXT_PUBLIC_` to expose to the client.

24. ## **How does Next.js support internationalization (i18n)?**

    - Configure in `next.config.js`.
    - Supports locale subpaths (`/en`, `/fr`).
    - Detects browser language automatically.

25. ## **How to optimize performance in Next.js?**

    - Use Image optimization.
    - Use dynamic imports (`next/dynamic`).
    - Cache data with ISR.
    - Enable compression/CDN.
    - Minimize bundle size.

26. ## **What is Dynamic Import in Next.js?**

    - Load components lazily using `next/dynamic`.

    ```ts
    import dynamic from 'next/dynamic'
    const Chart = dynamic(() => import('../components/Chart'), { ssr: false })
    ```

27. ## **How do you do authentication in Next.js?**

    - Common libraries: `NextAuth.js`, `Auth0`, `Firebase`.
    - With Middleware for protecting routes.
    - Store JWT in cookies or sessions.

28. ## **What are Edge Functions in Next.js?**

    - Run at the edge (`CDN`), closer to the user.
    - Low latency, great for personalization and auth.
    - Example: Middleware runs as edge functions.

29. ## **How do you deploy a Next.js app?**

    - Platforms: `Vercel (official)`, Netlify, AWS, Fly.io, Cloudflare Pages.
    - `next build && next start` for Node.js hosting.

30. ## **What is the difference between Client Components and Server Components in Next.js 13?**

    - **Server Components**: default, run on server, no client JS.
    - **Client Components**: opt-in with `"use client"` at the top, used for
      interactivity (state, hooks, event listeners).
