# How React Works Under the Hood.

## Source: 
https://medium.com/@ruchivora16/react-how-react-works-under-the-hood-9b621ee69fb5

## The Render Phase (Asyncronous & Non-blocking)
When the component initailly mounts or state changes, React triggers the **Render Phase**.
- React executes your compoent function to generate a new vertual DOM representing the updated UI.
- It triggers the **Diffing Algorithm** to compare the work in Progress with the current tree that is alredy on the screen.
- To do this quickly react uses a heuristic alogithm with O(N) complexity.

## The Commit Phase (Synchronous & Blocking)
Once the **Diffing Algorithm** figures out the minimal set of changes needed, React moves to the **Commit Phase**.

- React handover the list of changes to the platform specific renderer (like ReactDOM for web or React Native for mobile).
- The renderder mutates the actual **Real DOM** by appending deleting or updating the specific HTML nodes. Becuase the actual DOM updates are slow and expensive, batching them into a single commit minimizes layout reflows and repaints in the browser.


## Cleanup and Effects
Once the Real DOM matches the Virtual DOM, the browser paints the screen. Immeditely following this:

- React runs compoent lifecycle and hooks
- Synchronous layout effects (useLayoutEffect) fire right before the paint, while standard asynchornous effect (useEffect) fire right after the paint, so they do not block the user experiance.


## Strategies for Optimizing ReactJS Reconciliation
#### Use React.memo: 
Prevents re-renders in functional components when props don’t change using React.memo().

#### Use key Prop Efficiently in Lists: 
Assign unique keys to items in React lists to help efficiently update only changed elements.

#### Avoid Inline Functions/Objects: 
Inline functions/objects in JSX recreate every render, triggering re-renders; move them outside or memoize with useCallback.

#### Use React.PureComponent: 
React.PureComponent uses shallow prop/state comparison to prevent unnecessary re-renders.
