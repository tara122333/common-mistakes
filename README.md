# 📄 75 Common React.js Frontend Mistakes (With Solutions + Simple Examples)
React.js • Tailwind CSS • Redux • UI Components • TypeScript

## 1. Not Splitting Components Properly
- Mistake: Developers often write very long components ( 400 - 600 lines of code ) that handle everything: API calls, logic, UI, validation, etc. This becomes hard to maintain.
- Solution:
Split the component into smaller parts:
Container → Handles logic
UI Component → Handles design only

## 2. Incorrect useEffect Dependencies
- Mistake: If you forget the dependency array or use the wrong dependencies, React keeps re-running forever.
- Solution:
Add correct dependencies OR memoise functions.
- Example:
  ```
  ❌ Causes infinite re-render
  useEffect(() => {
    fetchData();
  });
  ```
  ```
  ✅ Use dependency array
  useEffect(() => {
    fetchData();
  }, []);
  ```

## 3. Not Cleaning Up useEffect
- Mistake: Timers, event listeners, or sockets cause memory leaks if not removed.
- Solution:
Return a cleanup function.
- Example:
  ```
  ❌ Bad
  useEffect(() => {
    window.addEventListener("resize", doSomething);
  }, []);
  ```
  ```
  ✅ Good
  useEffect(() => {
    window.addEventListener("resize", doSomething);
    return () => window.removeEventListener("resize", doSomething);
  }, []);
  ```

## 4. Not Handling Loading & Error States
- Mistake: Only showing success UI makes the app feel broken.
- Solution:
Show loading, error, and empty states.
- Example:
  ```
  if (loading) return <p>Loading...</p>;
  if (error) return <p>Error fetching data</p>;
  if (!data.length) return <p>No records found</p>;
  ```

## 5. Not Debouncing Search Input
- Mistake: API calls trigger on every key press → performance issues.
- Solution:
Use debounce.
- Example:

  `const debouncedSearch = useCallback(debounce(searchFn, 500), []);`

## 6. Poor Folder Structure
- Mistake: Putting all components in one folder becomes messy.
- Solution:
Use feature-based structure:
  ```
  /component
    - button.jsx
    - input.js
  /services
    - index.ts
  /pages
    - index.ts
    - user.ts
    - auth.ts
  /utils
    - index.ts
  ```

## 7. Writing Complex Logic Inside JSX
- Mistake: Doing loops or conditions inside return causes clutter.
- Solution:
Compute values before returning JSX.
- Example:
  ```
  const filtered = users.filter(u => u.age > 18);
  return filtered.map(u => <UserCard user={u} />);
  ```

## 8. Using Redux for Small Local States
- Mistake: Storing input fields/temporary data in Redux adds complexity.
- Solution:
Use local state unless it's global.

## 9. Not Normalizing Redux State
- Mistake: Nested objects are hard to update.
- Solution:
Normalize:
  ```
  {
    usersById: { "1": {...} },
    userIds: ["1"]
  }
  ```

## 10. Wrong Use of Tailwind Responsive Classes
- Mistake: Not adding `sm:`, `md:`, `lg:` leads to broken UI on mobile.
- Solution:
Use mobile-first design.

## 11. Hardcoding Colors & Styles
- Mistake: Inconsistent theme and unmaintainable UI.
- Solution:
Use Tailwind theme config.

## 12. Not Creating Reusable UI Components
- Mistake: Copy-pasting code leads to bugs.
- Solution:
Create reusable UI:

  `<Button variant="primary" />`


## 13. Poor Form Handling
- Mistake: Manually handling forms = too much code.
- Solution:
Use React Hook Form or use `formik` to handle form data.
- Example:

  `const { register } = useForm();`

## 14. Missing Validation
- Mistake: Invalid data goes to backend.
- Solution:
Use Yup or Zod.

## 15. Not Optimizing Images
- Mistake: Large images slow the app.
- Solution:
Use WebP + lazy loading.

## 16. Creating State That Never Changes
- Mistake: Developers put static values inside useState even when they never change.
- Solution:
Use normal variables or constants outside component.

## 17. Re-rendering Entire Component on Every Typing
- Mistake: Putting big components inside the parent of an input forces all children to re-render with every keystroke.
- Solution:
Split into small components and memoize.

## 18. Ignoring API Error Response Structure
- Mistake: Developers only log errors instead of handling them.
- Solution:
Use:
error.response?.data?.message

## 19. Fetching API in Every Component Instead of Sharing Data
- Mistake: Makes duplicate API calls.
- Solution:
Use React Query or Redux for shared data.

## 20. Creating Unnecessary Global State
- Mistake: Putting small UI logic in global store slows down app.
- Solution:
Only globalize what is truly global.

## 21. Keeping Large Objects in Redux Store
- Mistake: Storing huge API responses increases memory usage.
- Solution:
Store only required fields.

## 22. Not Using Suspense and Lazy Loading
- Mistake: Loading entire app at once increases load time.
- Solution:
Use:
const Dashboard = React.lazy(() => import("./Dashboard"));

## 22. Fetching API on Every Re-render
- Solution:
Always add dependency array to useEffect.

## 23. Using any Everywhere in TypeScript React
- Mistake: Removes type safety.
- Solution:
Use proper interfaces and types.

## 24. Using window.location.href for Navigation
- Mistake: Causes full reload.
- Solution:
Use:
`navigate("/dashboard");`

## 25. Not Handling Slow API with Skeleton Loaders
- Mistake: Empty white UI looks broken.
- Solution:
Use skeleton UI.

## 26. Not Using Error Boundaries
- Mistake: React crashes on small UI errors.
- Solution:
Create:

  `class ErrorBoundary extends React.Component {...}`

## 27. Overfetching (Fetching Data Even If Not Needed)
- Solution:
Refetch only when necessary.

## 28. Using Too Many Libraries Instead of Writing Simple Logic
- Mistake: Bloat increases bundle size.
- Solution:
First evaluate if a library is needed.

## 29. Not Removing Console Logs Before Production
- Mistake: Leads to leaks and slows production.
- Solution:
Remove logs or use logger utility.

## 30. Not Handling Empty API Responses
- Solution:
If no data → show empty UI instead of crashing.

## 31. Not Handling Pagination Properly
- Mistake: Loading entire dataset creates performance issues.
- Solution:
Use server-side pagination.

## 32. Not Validating API Response Before Using
- Mistake: App crashes when backend gives unexpected data.
- Solution:
Check:
if (!Array.isArray(data)) return;

## 33. Creating Axios Instance Inside Component
- Mistake: New instance created each re-render.
- Solution:
Create instance in separate file `(service.ts file)`.

## 34. Forgetting Dependency in useCallback
- Mistake: Causes stale values.

## 35. Using LocalStorage Without JSON.parse/Stringify Properly
- Example (❌ Wrong):
`localStorage.setItem("user", user);`

- Solution:
`JSON.stringify(user)`

## 36. Using indexOf or includes for Object Comparison
- Mistake: These only work for primitive types.
- Solution:
Use find().

## 37. Calling setState in a Loop
- Solution:
Batch updates or combine.

## 38. Using CSS Instead of Tailwind Utility Classes
- Mistake: Mixing styling methods makes UI inconsistent.
- Solution:
Stick to one styling system.

## 39. Making API Calls Directly in JSX
- Example (❌ Wrong):
<div>{fetchUsers()}</div>

- Solution:
Always fetch inside effects or React Query.

## 40. Using setState With Previous Value Without Callback
- Example (❌ Wrong):
`setCount(count + 1)`

- Solution:
`setCount(prev => prev + 1);`

## 41. Not Using Fragments Instead of Extra Divs
Problem
Too many nested <div> elements.
- Solution:
  Use:
  ```
  <>
  </>
  ```

## 42. Passing Unnecessary Props
- Mistake: Causes unnecessary re-renders.
- Solution:
Use props only when needed.

## 43. Not Using Prettier / ESLint
- Mistake: Code becomes messy and inconsistent.
- Solution:
Enable Prettier + ESLint.

## 44. Writing Long Conditional Rendering
- Example (❌ Wrong):

  `{isLoggedIn ? <Dashboard /> : x ? <X/> : y ? <Y/> : <Login />}`

- Solution:
Extract logic into helper.

## 45. Using Unoptimized Loops
- Mistake: Nested loops inside render slow down UI.
- Solution:
Preprocess data outside render.

## 46. Using Too Many Inline Styles
- Mistake: Inline styles override Tailwind and break responsive UI.

## 47. Not Handling Promise Rejection
- Example (❌ Wrong):
axios.get("/api");

- Solution:
Always handle .catch() or try/catch.

## 48. Hardcoding Colors Instead of Theme Colors
- Mistake:
Using custom hex codes everywhere.

  ```jsx
  <div className="text-[#3482ff]">Wrong</div>
  ```

- Solution:
Use Tailwind theme colors.

  ```jsx
  <div className="text-blue-500">Correct</div>
  ```

## 49. Using “mt-10 mb-10” Instead of “my-10”
- Mistake:
Repeating utility classes unnecessarily.

- Solution:

  ```jsx
  <div className="my-10" />
  ```


## 50. Incorrect Flex or Grid Usage
- Mistake:
Writing both `flex` & `grid`.

- Solution:
Use one system per container.


## 51. Wrong Ordering of Classes
- Mistake:
Responsive classes must be placed after base ones.

**Wrong (ignored override):**

  ```jsx
  <div className="p-10 sm:p-4"></div>
  ```

**Correct:**

  ```jsx
  <div className="p-4 sm:p-10"></div>
  ```


## 52. Not Using Group & Group-Hover
- Mistake:
Hovering parent doesn’t style children.

- Solution:

  ```jsx
  <div className="group">
    <p className="opacity-0 group-hover:opacity-100">Hello</p>
  </div>
  ```


## 53. Manually Adding Spacing Between Elements
- Mistake:

  ```jsx
  <div className="space-y-4">
    <div className="mb-4">Item</div>
  ```

- Solution:

Use Tailwind's `space-y-` classes.


## 54. Forgetting To Use Aspect-Ratio
- Mistake:
Incorrect image/video scaling.

- Solution:

  ```jsx
  <div className="aspect-video">
    <iframe ... />
  </div>
  ```


## 55. Wrongly Centering Elements
- Mistake:

  ```jsx
  <div className="text-center"></div>
  ```

When trying to center blocks.

- Solution:

  ```jsx
  <div className="flex justify-center items-center" />
  ```


## 56. Using Incorrect Utility Combinations
- Example:

  ```jsx
  <div className="items-center"></div>  // missing flex
  ```

- Solution:

  ```jsx
  <div className="flex items-center" />
  ```


## 57. Not Using Tailwind’s Arbitrary Values
- Mistake:
Creating custom CSS just to change a value.

- Solution

  ```jsx
  <div className="w-[450px] h-[320px]" />
  ```


## 58. Not Removing Dead & Duplicate Classes

- Example (common mess):

  ```jsx
  <div className="px-4 px-6 py-2 p-4"></div>
  ```

- Solution:
Lint classes → consider **Prettier Tailwind plugin**.


## 59. Not Typing Component Props

- Mistake:

  ```ts
  const UserCard = (props) => { ... }
  ```

- Solution

  ```ts
  type Props = { name: string; age?: number };
  const UserCard = ({ name, age }: Props) => { ... }
  ```

## 60. Incorrect Use of `useState` Types

- Mistake:

  ```ts
  const [name, setName] = useState(null); // becomes null | string
  ```

- Solution

  ```ts
  const [name, setName] = useState<string | null>(null);
  ```

## 61. Using Broad Types Like `object`, `{} `

- Mistake:
`{}` means anything except null/undefined → useless.

- Solution
Use interfaces:

  ```ts
  interface User { id: number }
  ```

## 62. Not Typing Event Handlers

- Mistake:
Using `any` for events.

- Solution

  ```ts
  const handleChange = (e: React.ChangeEvent<HTMLInputElement>) => {}
  ```

## 63. Incorrectly Typing API Responses

- Mistake:
Assuming backend always returns correct structure.

- Solution

  ```ts
  interface ApiUser {
    id: number;
    name: string;
  }
  ```

## 64. Bad Typing for Axios

- Mistake:

  ```ts
  const res = await axios.get("/users"); // res: any
  ```

- Solution

  ```ts
  axios.get<User[]>("/users");
  ```

## 65. Not Typing Children Properly

- Mistake:

  ```ts
  children: any
  ```

- Solution

  ```ts
  children: React.ReactNode
  ```

## 66. Writing Return Types Implicitly

- Mistake:
Hard to detect wrong returns.

- Solution

  ```ts
  function sum(a: number, b: number): number {
    return a + b;
  }
  ```

## 67. Typing Props and State Separately
- Mistake:
Duplicated code.

- Solution
Use a single type and reuse.

## 68. Using Wrong Type for `ref`
- Mistake:

  ```ts
  const ref = useRef(null);
  ref.current.value // ❌ TS error
  ```

- Solution

  ```ts
  const inputRef = useRef<HTMLInputElement>(null);
  ```

## 69. Overusing `| null` Instead of Good Defaults
- Mistake:
Too many nullable types cause runtime issues.

- Solution
Use default values when possible.

## 70. Not Using `Pick` / `Omit` / `Partial` / `Required`
- Mistake:
Manually rebuilding types instead of composing.

- Solution

  ```ts
  type UserPreview = Pick<User, "id" | "name">
  ```

## 71. Forgetting to Type Async Function Returns
- Mistake:
Async functions return `Promise<any>`.

- Solution

  ```ts
  async function getUser(): Promise<User> {}
  ```

## 72. Typing Arrays Incorrectly
- Mistake:

  ```ts
  const items: [] = []; // ❌ empty tuple
  ```

- Solution

  ```ts
  const items: User[] = [];
  ```
