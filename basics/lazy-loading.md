# Lazy Loading in React ([source](https://www.geeksforgeeks.org/reactjs/lazy-loading-in-react-and-how-to-implement-it/))

Lazy loading is a performance optimization technique that load only the required content initially, improving page load speed. Additional components, images or scripts are loaded only when needed, such as on user interation or scrolling.

- Improves application performance by reducing `initial load time`.
- Loads components, modules or assets `asynchronously` when required.
- Implemented using `React.lazy()` along with Suspence component.


## Syntax
```jsx
// import Suspence and lazy components
import { Suspense, lazy } from "react";

// import the component you want to lazy load
const MyComponent = React.lazy(() => import('./MyComponent'));


// Wrap the imported component in the Suspence component with fall back UI
<Suspence  fallback={<div>Loading...</div>}>
    <MyComponent />
</Suspence>
```


Components are loaded only when requested, reducing the initial bundle size.