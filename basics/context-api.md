# Provider Component
In React, provider is a special component used to share data globally across your component tree without having to pass the props down manually through every single level.

This design strategy is called **Provider Pattern**, and it is the primary solution for the problem of "prop drilling".

# Implementaion (Context API)
To use a Provider, you follow three basic steps:

1. **Create a Context**
2. **Provide a Value:** Wrap your components with a `.Provider` compoennt and pass the data into its `value` prop.
3. **Consume the Value:** Use the `useContext` hook in any of the child component to read the data.


```jsx
import React, { createContext, useContext, useState } from 'react';

// 1. Create the Context
const ThemeContext = createContext();

export default function App() {
    const [theme, setTheme] = useState('dark');

    return (
        // 2. The Provider component broadcasts the theme state down the tree
        <ThemeContext.Provider value={{ theme: setTheme }}>
            <Navbar />
            <MainContent>
        </ThemeContext.Provider>
    );
}
```
```jsx
function MainContent() {
    // This intermediate component doesn't need to know anything about the theme at all!
    return (
        <Button />
    )
}
```
```jsx
function Button() {
    // 3. The deeply nested child consumes the value directly using a hook
    const { theme, setTheme } = useContext(ThemeContext);

    return (
        <button className={`btn-${theme}`}>
            Current Theme: {theme}
        </button>
    );
}
```

# When to Use a Provider Component
Provider components are ideal for data that needs to be accessed by many components spread across different parts of your application. Common user cases include:

- Global Themes
- User Authentication
- Languate/Localization
- Global State Management

# Key Behavious to keep in Mind
- **Automate Reneders:**
Everytime the `value` prop of the Provider component changes, all the child components that are consuming that context will automaically rerenders to reflect the newest data.

# TakeAway
Together, Providers and Consumers facilitate the management of global state and makes it easy to share data between components in a React application, ultimately improving code maintainability and reducing prop drilling.