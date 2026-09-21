# Vertualization in React: Improving performance for Large Lists ([source](https://medium.com/@ignatovich.dm/virtualization-in-react-improving-performance-for-large-lists-3df0800022ef))


Rendering large lists in React quickly need to performance bottlenecks, especially when dealing with thousands of elements. Virtualization is a technique that optimizes this by only rendering visible elements and efficiently managing  DOM updates.

We can implement this using `react-window`.
