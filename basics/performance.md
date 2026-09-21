# Performace Optimization in React

1. [lazy loading](basics/lazy-loading.md)
2. [virtualization for large lists](basics/virtualization.md)
    - useInsertionEffect
3. [use memoization]()
    - useCallback for linefunctions
    - useMemo to cache results of complex calculations.
4. Use `key prop` without fail in lists.


## gemini

### 🚀 1. Automated Optimization (Modern React)
The easiest way to gain massive performance enhancements is to integrate the **React Compiler**.

#### Automatic Memoization: 
The compiler automatically determines where to optimize code, removing the risk of poorly configured dependency arrays or over-memoization.Strict 

#### Rule Enforcement: 
It only optimizes components that strictly follow the Rules of Hooks. It automatically surfaces architectural mistakes that cause bugs or slow down code.

### 🧩 2. Code Splitting & Resource Management
Reducing your application's initial bundle size improves time-to-interactive scores and speeds up initial page loads.
#### Dynamic Imports: 
Use `React.lazy()` paired with Suspense to split massive routes or heavy UI blocks into smaller JavaScript chunks that load only when needed.
#### Fragment Architecture: 
Group nested components using React.Fragments (<>...</>) to prevent rendering extra, unneeded HTML wrapper DOM elements.🎨 

### 3. UI and List Rendering
Large collections of data can bottleneck the DOM tree if treated carelessly.
#### List Virtualization: 
For hundreds or thousands of list items, use windowing tools like react-window or react-virtualized. These only render the small viewport window visible to the user, saving huge amounts of memory.

#### Stable Keys: 
Always supply a unique, permanent identifier (such as an id) from your dataset as the key prop. Never use array indices as keys, as shifting indices force React to mistakenly destroy and re-create DOM nodes.

### 📉 4. Traditional Memoization (Manual Patterns)
If you aren't using the React Compiler yet, you must carefully handle component updates using manual memoization tools:

 Outer pipes  Cell padding 
No sorting
| **Tool**          | **Primary Purpose**        | **How It Optimizes**                                                                                  |
| ----------------- | -------------------------- | ----------------------------------------------------------------------------------------------------- |
| **React.memo()**  | Component-level wrapper    | Shallowly compares props and blocks unnecessary functional component re-renders.                      |
| **useMemo()**     | Caches expensive values    | Memorizes the result of intensive synchronous calculations, skipping execution if dependencies match. |
| **useCallback()** | Caches function references | Stores function instances across renders so children receiving them as props don't break memoization. |

_Note: Avoid declaring anonymous or inline functions inside your JSX templates. This continually re-allocates function memory references on every render cycle._

### 🛠️ 5. Diagnostics: Profile Before Modifying
Never apply manual optimizations blindly, as misapplied hooks can actually create performance penalties. Use the **React DevTools Profiler** tab to record interactions, trace why a component re-rendered, and isolate actual bottlenecks.

---

### Writing Hooks: Do you still need useMemo and useCallback?

⚠️ Strict Rules or Bypassed Code: The compiler will only optimize code if it can safely prove it follows the "Rules of React" (e.g., component purity, no direct mutations). If a component breaks these rules, the compiler will quietly skip it to prevent breaking your app. In those skipped files, you would still need manual hooks.

🔌 Third-Party Libraries: If a third-party library or an external SDK specifically demands a strictly stable function or reference dependency that the compiler's heuristics didn't catch, you will still need to use useCallback or useMemo manually.

📈 Extreme Calculations: For massive, highly intensive synchronous calculations, leaving an explicit useMemo signals your direct structural intent to other developers and guarantees that the cache persists exactly as you intended.

#### Take away
You should stop using `useMemo` and `useCallback` preemptively. Write clean, standard React code first, let the compiler do its job, and only add the manual hooks if performance profiling proves a specific bottleneck remains.