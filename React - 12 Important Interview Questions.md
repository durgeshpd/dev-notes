React - 12 Important Interview Questions

1. Hooks
- Hooks are special JavaScript functions provided by React. They allow you to use features like state and lifecycle in function components.
	- Commonly used Hooks:
		- useState()
		- useEffect()
		- useContext()
		- useReducer()
		- useMemo()
		- useRef()

	- The most commonly used hooks are useState() and useEffect().

(1) useState()
    - useState is a React Hook that lets you add state to a function component.
    - It returns an array with two values:
        1. The current state value
        2. A function to update that value

    Example:
    ```bash 
    import React, { useState } from 'react';

    function Counter() {
      const [count, setCount] = useState(0);

      return (
        <div>
          <p>You clicked {count} times</p>
          <button onClick={() => setCount(count + 1)}>
            Click me
          </button>
        </div>
      );
    }
    ```

==> Common Interview Follow-up Questions for useState:

1. What is useState?
- It’s a Hook to store and update local state in function components.

2. What does useState() return?
- An array: [state, setStateFunction]

3. What types of data can useState hold?
- Strings, numbers, booleans, arrays, objects – any data type.

4. What happens when you call the setter (setState)?
- React updates the state and re-renders the component.

5. How to update state based on previous value?
- Use a callback:
  setCount(prev => prev + 1);

6. What if you call useState() with no value?
- Initial value will be undefined.

7. Is useState asynchronous?
- Yes. State updates don't happen instantly.

8. Can we use useState inside a loop or condition?
- ❌ No. Hooks must be used at the top level only.

9. Difference between useState, useRef, and useReducer?
- useState: causes re-render.
- useRef: holds value without re-render.
- useReducer: handles complex state logic.

10. Can useState take a function as default value?
- ✅ Yes, for lazy initialization:
  useState(() => heavyFunction());

11. Is there a dependency array in useState?
- ❌ No. Dependency arrays are only used in useEffect.

12. Does React always re-render on setState?
- Only if the new value is different from the current value.


(2) useEffect()
	- useEffect is a React Hook that lets you run side effects in function components.
	- Side effects include:
		- Fetching data
		- Updating the DOM manually
		- Setting up subscriptions or timers
		- Logging
	- It runs after the component renders.

	Syntax:
 	```bash
	useEffect(() => {
	// side effect code here
	}, [dependencies]);

	Example:
 	```bash
	import React, { useState, useEffect } from 'react';

	function Timer() {
	const [count, setCount] = useState(0);

	useEffect(() => {
		const interval = setInterval(() => {
		setCount(prev => prev + 1);
		}, 1000);

		// Cleanup when component unmounts
		return () => clearInterval(interval);
	}, []);

	return <h1>{count}</h1>;
	}
 	```

==> Common Interview Follow-up Questions for useEffect:

1. What is useEffect?
- A hook used to run side effects in function components.

2. When does useEffect run?
- After every render by default.
- But you can control it with the dependency array.

3. What is the dependency array in useEffect?
- It tells React when to re-run the effect.
  - [] → run only once on mount (like componentDidMount)
  - [var] → run when var changes
  - no array → run on every render

4. What happens if dependency array is empty []?
- The effect runs only once — after the first render.

5. What happens if there's no dependency array at all?
- The effect runs after every render.

6. What if I return a function from useEffect?
- That function is called the "cleanup function".
- It runs when the component unmounts or before the effect re-runs.

7. Can I use async/await in useEffect?
- Not directly. You should define an async function inside the effect and call it.

	Example:
	```bash
	useEffect(() => {
	const fetchData = async () => {
		const res = await fetch(url);
		const data = await res.json();
		setData(data);
	};
	fetchData();
	}, []);
 	```

8. Can you have multiple useEffect() in one component?
- ✅ Yes. Each useEffect is independent.

9. What’s the difference between useEffect and useLayoutEffect?
- useEffect runs after the DOM is painted.
- useLayoutEffect runs before the paint — it can block the browser, used for layout adjustments.

10. What causes useEffect to re-run?
- Changes to any value in the dependency array.

(3) useContext()
	- Accesses values from React Context (avoids props drilling).
	📌 Syntax:
 
	```bash
	const value = useContext(MyContext);
 	```
	
	✅ Example:
 
 	```bash
	const ThemeContext = React.createContext("light");

	function App() {
	return (
		<ThemeContext.Provider value="dark">
		<Child />
		</ThemeContext.Provider>
	);
	}

	function Child() {
	const theme = useContext(ThemeContext);
	return <div>Theme is {theme}</div>;
	}
 	```
	
(4) useRef()
	- Creates a mutable reference that doesn’t trigger re-renders.

✅ Common Uses:
	- Accessing DOM nodes (inputRef.current.focus())
	- Keeping values between renders (like prevValue)

	📌 Example:
 	```bash

	const inputRef = useRef();

	useEffect(() => {
	inputRef.current.focus();
	}, []);

	return <input ref={inputRef} />;
 	```
	
(5) useMemo()
	- Memoizes the result of a calculation — used to avoid re-computing expensive functions on every render.

	📌 Example:
 	```bash

	const expensiveValue = useMemo(() => {
	return heavyCalculation(num);
	}, [num]);
 	```
	
(6) useCallback()
	- Memoizes a function — avoids creating a new function on every render.

	📌 Example:
 	```bash

	const handleClick = useCallback(() => {
	console.log("Clicked");
	}, []);
	
7. useReducer()

	- Like useState, but for complex state logic (similar to Redux reducer).

	📌 Example:
	```bash

	function reducer(state, action) {
	switch (action.type) {
		case 'increment':
		return { count: state.count + 1 };
		default:
		return state;
	}
	}

	const [state, dispatch] = useReducer(reducer, { count: 0 });
 	```

📌 Section: Commonly Asked Hooks Q&A

🔹 useContext
Q: What problem does useContext solve?
A: It solves the problem of props drilling, where data needs to be passed through many nested components. useContext lets you access shared state directly without passing it manually at every level.
✅ Best for: Theme, Language, Auth, User data, etc.

🔹 useRef
Q: What is useRef used for?
A: 
- Access DOM elements (like inputRef.current.focus()).
- Store a value that doesn’t trigger re-render.
	- Example: previous props, timers, intervals, etc.
✅ Think of useRef as a box to store any value across renders without causing re-renders.

🔹 useMemo
Q: When should we use useMemo?
A: Use it to optimize performance by caching the result of a heavy calculation. React will skip re-running the function if dependencies haven’t changed.
✅ Best for:
	- Expensive calculations
	- Preventing unnecessary renders

 	```bash
	const expensiveValue = useMemo(() => computeValue(num), [num]);
	
🔹 useCallback
Q: What is useCallback and why use it?
A: useCallback returns a memoized version of a function. Useful to prevent unnecessary re-renders of child components that depend on that function.
✅ Best for:
	- Passing stable function references to optimized child components
	- Preventing re-renders caused by new function identities on every render

 	```bash

	const handleClick = useCallback(() => {
	console.log("Clicked");
	}, []);
 	```
	
🔹 useReducer
Q: Why use useReducer over useState?
A:
- Use useReducer when you have complex state logic, like:
	- Multiple state variables that depend on each other
	- Complex updates (e.g., reset, undo, nested updates)
✅ Cleaner than multiple useState calls in large components.

Example:
```bash
function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };
    default:
      return state;
  }
}

const [state, dispatch] = useReducer(reducer, { count: 0 });
```


2. Virtual DOM

What is the DOM?

	- **DOM (Document Object Model)**: A tree structure that represents HTML elements in memory.
	- It's how the browser represents the web page, allowing interaction with its content.

	**Example of DOM structure:**

	```bash
	<html>
	<head>
		<title>Page Title</title>
	</head>
	<body>
		<div>
		<h1>Hello, World!</h1>
		</div>
	</body>
	</html>
	```
	
What is the Virtual DOM?
	- Virtual DOM: A lightweight copy of the real DOM kept in memory by React.
	- React updates the Virtual DOM first and then efficiently applies the changes to the real DOM.
	- The Virtual DOM makes updates faster by avoiding direct manipulation of the real DOM (which is slow).

How does the Virtual DOM work?
	- When state or props change, React creates a new Virtual DOM tree.
	- React compares the new tree with the previous one and determines what parts have changed.
	- React then updates only the changed parts in the real DOM.
	- This process is called reconciliation.

Reconciliation Algorithm (React Fiber)
	- Reconciliation: The process of updating the real DOM with the minimum number of changes.
	- React Fiber: A new reconciliation algorithm introduced in React 16 to improve performance.

Key Features of React Fiber:
	- Asynchronous rendering: Breaks rendering into smaller chunks, improving responsiveness.
	- Prioritization: Handles high-priority updates before low-priority ones.
	- Error boundaries: Better handling of errors in components.

Difference between Virtual DOM and Real DOM
	Real DOM:
	- Directly updates the browser's layout, which is slow.
	- Re-renders the entire UI on every state change.
	
	Virtual DOM:
	- A lightweight copy of the DOM that minimizes direct DOM manipulation.
	- React updates only the parts that have changed, making it faster.

React Fiber and the Diffing Algorithm
	- Diffing Algorithm: React compares the new Virtual DOM with the previous one to identify changes.

	How it works:
	- Create a virtual DOM tree for the current state.
	- Compare it with the previous tree.
	- Identify differences (additions, deletions, updates).
	- Apply only those changes to the real DOM.
	- React Fiber optimizes this algorithm by making it more efficient and asynchronous.

Key Takeaways
	- Virtual DOM: Reduces direct manipulation of the real DOM for better performance.
	- Reconciliation: Determines the minimal changes required to update the real DOM.
	- React Fiber: Introduces asynchronous rendering and prioritization to improve performance.

Common Interview Follow-up Questions for Virtual DOM:

What is the difference between the real DOM and the virtual DOM?
	- Real DOM: Direct interaction with the actual DOM; slower updates.

Virtual DOM: A lightweight copy of the DOM; React uses it to minimize DOM changes.
	- What is the purpose of the React Fiber algorithm?

React Fiber is designed to improve the performance of the reconciliation process. It makes rendering asynchronous, allows prioritization of updates, and reduces UI jank.
	- How does React determine what has changed in the Virtual DOM?

React compares the new Virtual DOM with the previous one using the diffing algorithm. It then applies only the necessary changes to the real DOM.
	- What is the diffing algorithm in React?
	- It’s the process React uses to compare the current Virtual DOM with the previous one. React then determines the minimum number of changes needed and applies those changes to the real DOM.
	
Why is React’s Virtual DOM faster than direct DOM manipulation?
	- The Virtual DOM reduces the number of direct DOM manipulations, which are costly in terms of performance. React can update only the changed parts of the real DOM, rather than re-rendering the entire UI.


3. Component Lifecycle Methods

What is a Lifecycle Method?

	- Lifecycle methods in React allow you to run specific code at different stages of a component's life.
	- These methods are available for **class components**. For **function components**, React **Hooks** like `useEffect()` replicate similar behavior.

Class Components vs Function Components

	What is a Class Component?

	- **Class Component**: A JavaScript class that extends `React.Component` and uses lifecycle methods to manage component behavior (e.g., `componentDidMount()`, `componentDidUpdate()`).
	- **Class components** were traditionally used to manage state, lifecycle methods, and UI behavior.

	Why Function Components are Preferred Now

	- With the introduction of **React Hooks** (like `useState`, `useEffect`), **function components** can now manage state, side-effects, and lifecycle-like behavior without the need for class-based components.
	- Function components are simpler and shorter in syntax.

Example of Counter Component

Class Component:

	```bash
	import React, { Component } from 'react';

	class CounterClass extends Component {
	constructor(props) {
		super(props);
		this.state = { count: 0 };
	}

	increment = () => {
		this.setState({ count: this.state.count + 1 });
	};

	componentDidMount() {
		console.log('Class Component Mounted');
	}

	componentDidUpdate(prevProps, prevState) {
		console.log('Class Component Updated');
	}

	render() {
		return (
		<div>
			<p>You clicked {this.state.count} times</p>
			<button onClick={this.increment}>Click me</button>
		</div>
		);
	}
	}

	export default CounterClass;
	```
	
	
Function Component with Hooks:

	```bash
	import React, { useState, useEffect } from 'react';

	function CounterFunction() {
	const [count, setCount] = useState(0);

	useEffect(() => {
		console.log('Function Component Mounted');
	}, []); // Empty array means only runs once, like componentDidMount

	useEffect(() => {
		if (count !== 0) {
		console.log('Function Component Updated');
		}
	}, [count]); // Runs on count change, like componentDidUpdate

	return (
		<div>
		<p>You clicked {count} times</p>
		<button onClick={() => setCount(count + 1)}>Click me</button>
		</div>
	);
	}

	export default CounterFunction;
	```
	
	
Component Lifecycle Phases

	- Mounting: When the component is being created and inserted into the DOM.

	Updating: When the component is being re-rendered due to state or props changes.

	Unmounting: When the component is being removed from the DOM.

	Mounting (Initial Render)
	Lifecycle Methods for Mounting:

	constructor(): Initializes state and binds methods.

	static getDerivedStateFromProps(): Called before rendering when props change.

	render(): Returns JSX for the component.

	componentDidMount(): Runs after the component is mounted (when the component is inserted into the DOM).

	- Updating (Re-rendering)
	Lifecycle Methods for Updating:

	static getDerivedStateFromProps(): Updates state based on props changes.

	shouldComponentUpdate(): Decides if a component should re-render.

	render(): Re-renders the component.

	getSnapshotBeforeUpdate(): Captures values before the update.

	componentDidUpdate(): Runs after the component is updated.

	- Unmounting (Removal)
	Lifecycle Method for Unmounting:

	componentWillUnmount(): Cleanup (e.g., cancel subscriptions, clear timers) just before the component is removed from the DOM.

Common Interview Follow-up Questions for Lifecycle Methods:

What is the lifecycle of a React component?
	- A React component goes through three main phases: Mounting, Updating, and Unmounting.

What is the purpose of componentDidMount()?
	- It is called once the component is mounted and rendered. Useful for fetching data or setting up subscriptions.

What is shouldComponentUpdate() used for?
	- Optimizes re-rendering by deciding if the component should update based on state/props changes.

What is the difference between componentDidUpdate() and componentWillUnmount()?
	- componentDidUpdate() runs after the component updates, while componentWillUnmount() is called before the component is removed from the DOM.

Can I use lifecycle methods in functional components?
	- No, lifecycle methods like componentDidMount() are only for class components. In function components, use the useEffect() hook to manage side-effects.
	
	
4. Lazy Loading

What is Lazy Loading?
	- Lazy Loading is a design pattern in React where components, routes, or resources are only loaded when they are needed, instead of loading everything upfront.
	- This improves the performance of a React app by reducing the initial loading time and loading only the necessary parts of the app as the user interacts with it.

Why Use Lazy Loading?
	- Optimizes Performance: Reduces the initial bundle size by loading only the essential code at first, and loading other parts when required.
	- Better User Experience: The user can start interacting with the app without waiting for the entire application to load.

How Does Lazy Loading Work in React?
React.lazy():

This function allows you to dynamically import a component only when it’s needed.

Suspense:

This component is used to handle the loading state (like a loading spinner) while the component is being fetched asynchronously.

React Lazy Loading Example:
Step 1: Using React.lazy() for Lazy Loading Components

	```bash
	import React, { Suspense } from 'react';

	// Lazy load the component
	const MyComponent = React.lazy(() => import('./MyComponent'));

	function App() {
	return (
		<div>
		<h1>Welcome to Lazy Loading Example</h1>
      
		{/* Wrap the lazy-loaded component in Suspense */}
		<Suspense fallback={<div>Loading...</div>}>
			<MyComponent />
		</Suspense>
		</div>
	);
	}

	export default App;
	```
	
Explanation:
React.lazy():

This function loads MyComponent only when it's rendered for the first time.

Suspense:

While MyComponent is being loaded, the fallback component (<div>Loading...</div>) will be shown to the user. Once MyComponent is loaded, it will be rendered.

Step 2: Lazy Loading Routes with React Router (optional)
If you're using React Router and want to lazily load routes, you can combine React.lazy() with Suspense.

	```bash

	import React, { Suspense } from 'react';
	import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';
	
	// Lazy load the route components
	const Home = React.lazy(() => import('./Home'));
	const About = React.lazy(() => import('./About'));

	function App() {
	return (
		<Router>
		<div>
			<h1>React Lazy Loading with Routing</h1>

			{/* Wrap routes in Suspense */}
			<Suspense fallback={<div>Loading...</div>}>
			<Switch>
				<Route exact path="/" component={Home} />
				<Route path="/about" component={About} />
			</Switch>
			</Suspense>
		</div>
		</Router>
	);
	}

	export default App;
	```
	
Explanation:
React.lazy() is used to load Home and About components only when their respective routes are visited.

The Suspense component will show the Loading... text while these components are being loaded.

Common Interview Follow-up Questions for Lazy Loading:

What is React.lazy() used for?
	- React.lazy() allows components to be loaded dynamically only when they are rendered, rather than during the initial load. This optimizes app performance by reducing the size of the initial bundle.

What is the purpose of Suspense in lazy loading?
	- Suspense is used to wrap lazy-loaded components. It lets you specify a fallback UI (e.g., a loading spinner or message) that is displayed while the lazy-loaded component is being fetched.

Can lazy loading be used with React Router?
	- Yes, you can use React.lazy() to lazily load route components in combination with Suspense. This ensures that route components are only loaded when the user navigates to them.

What happens if there is an error in lazy loading?
	- If there is an error in loading a lazy component, you can handle it using ErrorBoundary or by using React.lazy with a try-catch block inside a Suspense component.

Can we use lazy loading for non-component assets like images or libraries?
	- Yes, you can use dynamic imports (import() syntax) for other assets, but lazy loading in React is primarily designed for components.

Is lazy loading supported in functional and class components?
	- Yes, lazy loading works with both functional and class components. However, it is more commonly used with functional components since hooks are used for managing state and side effects.

Key Takeaways about Lazy Loading:

	- React.lazy() dynamically loads components to optimize the app's initial load time.
	- Suspense is used to handle the loading state while a component is being fetched.
	- It improves the app's performance by splitting the JavaScript bundle into smaller chunks.
	- You can also use lazy loading with React Router for route-based code splitting.



5. Custom Hooks

✅ What is a Custom Hook?
	- A custom hook is a JavaScript function whose name starts with use and can call other hooks.
	- It allows you to extract reusable logic from a component.
	- Custom hooks help make your code cleaner, modular, and DRY (Don't Repeat Yourself).

✅ Why Use Custom Hooks?
	- To avoid repeating logic in multiple components.
	- To separate business logic from UI code.
	- To make complex components simpler and more readable.
	- Promotes code reusability.

✅ When to Use Custom Hooks?
	- Use a custom hook when:
	- You use the same useEffect, useState, or any other hook logic in multiple components.
	- You want to organize complex logic into smaller, maintainable parts.
	- You want to encapsulate side effects, fetching, timers, form logic, etc.

✅ How to Create a Custom Hook?
	- Custom hooks are just functions that use other hooks.
	- They start with the word use, like useFetch, useForm, useToggle.

📦 Example: Custom Hook – useOnlineStatus

	```bash
	// useOnlineStatus.js
	import { useState, useEffect } from 'react';

	function useOnlineStatus() {
	const [isOnline, setOnlineStatus] = useState(navigator.onLine)
	useEffect(() => {
		const goOnline = () => setOnlineStatus(true);
		const goOffline = () => setOnlineStatus(false);

		window.addEventListener("online", goOnline);
		window.addEventListener("offline", goOffline);

		return () => {
		window.removeEventListener("online", goOnline);
		window.removeEventListener("offline", goOffline);
		};
	}, []);

	return isOnline;
	}

	export default useOnlineStatus;
	```


How to use it in a component:

	```bash

	import React from 'react';
	import useOnlineStatus from './useOnlineStatus';

	function App() {
	const isOnline = useOnlineStatus();

	return (
		<div>
		{!isOnline && (
			<div style={{
			position: 'fixed',
			top: 0,
			width: '100%',
			backgroundColor: '#ff4d4f',
			color: '#fff',
			padding: '10px',
			textAlign: 'center',
			zIndex: 1000
			}}>
			🚫 Oops! You are offline.
			</div>
		)}
		<h1>My React App</h1>
		</div>
	);
	}

	export default App;
	```

	
🔄 Other Real-life Examples of Custom Hooks

Custom Hook			Description
useFetch()			For fetching API data
useForm()			For managing form state and handlers
useDebounce()		For debouncing input (e.g. search box)
useLocalStorage()	Sync state with localStorage
useTimer()			Custom timers/countdowns

🤔 Common Interview Follow-up Questions for Custom Hooks

What is a custom hook in React?
	- A custom hook is a function that uses built-in hooks and lets you reuse stateful logic between components.

Can custom hooks use other hooks like useState, useEffect?
	- ✅ Yes. They are functions built with other hooks.

Can we use a custom hook inside loops or conditions?
	- ❌ No. Like built-in hooks, custom hooks must also follow Rules of Hooks (only called at the top level of a function component or another hook).

What’s the benefit of using custom hooks over plain functions?
	- Plain functions can't use React hooks. Custom hooks allow you to use state, side effects, etc., and integrate them into React's lifecycle.

Do custom hooks cause re-renders?
	- No, the hook itself doesn’t cause a re-render — but if it uses useState or useEffect, those hooks can trigger updates just like in normal components.

Can custom hooks return JSX?
	- ❌ No. Custom hooks return data, functions, or values — not UI. Only components return JSX.

How do custom hooks improve code quality?
	- They help separate logic from UI, reduce duplication, improve maintainability and testability.

🔑 Key Takeaways

	- Custom Hooks = Reusable logic for multiple components.
	- Start with use, follow the Rules of Hooks.
	- Use when logic is repeated or too complex inside components.
	- Helps in clean, readable, maintainable code.
	
	
6. Higher Order Components (HOC)

✅ What is a Higher Order Component?

	- A Higher Order Component (HOC) is a function that takes a component and returns a new component with extra features or logic.
	- It is not a component itself, but a pattern in React.
	- Think of it like a wrapper that adds functionality.

✅ Why Use HOC?

	- To reuse logic between multiple components.
	- To add common behavior like logging, access control, API handling, etc.
	- Makes your code cleaner and DRY (Don't Repeat Yourself).

✅ When to Use HOC?

Use HOCs when:

	- Multiple components need the same logic or data (e.g., auth check, fetching data, etc.)
	- You want to apply cross-cutting concerns (e.g., tracking, analytics, permission checks).
	- You want to avoid duplicating logic across components.

✅ How to Create a HOC?

A HOC is a function like this:

	```bash
	const withExtraInfo = (WrappedComponent) => {
	return function EnhancedComponent(props) {
		// You can add logic here
		return <WrappedComponent {...props} />;
	};
	};
	```
	
🔧 Example: A Simple HOC that Adds a Message

	```bash
	// withMessage.js
	import React from 'react';

	function withMessage(WrappedComponent) {
	return function EnhancedComponent(props) {
		return (
		<div>
			<p>This is from HOC</p>
			<WrappedComponent {...props} />
		</div>
		);
	};
	}

	export default withMessage;
	```
	
Original Component:

	```bash
	// Hello.js
	import React from 'react';

	function Hello() {
	return <h2>Hello from Original Component</h2>;
	}

	export default Hello;
	```
	
Use the HOC:

	```bash
	// App.js
	import React from 'react';
	import Hello from './Hello';
	import withMessage from './withMessage';

	const EnhancedHello = withMessage(Hello);

	function App() {
	return (
		<div>
		<EnhancedHello />
		</div>
	);
	}

	export default App;
	```
	
	🧾 Output:

	This is from HOC
	Hello from Original Component
	
	
🤔 Common Interview Questions on HOC:

What is a Higher Order Component?
	- A function that takes a component and returns a new component with added behavior.

Why would you use HOC instead of just reusing logic in components?
	- HOCs help extract and share logic cleanly between components without modifying their code.

Do HOCs modify the original component?
	- ❌ No. They wrap and enhance the original component without changing it directly.

What are some real-world uses of HOCs?
	- Logging, authentication, theming, role-based access, tracking user behavior.

Can you use hooks inside HOCs?
	- ✅ Yes. If the HOC is a functional component, you can use hooks like useEffect, useState.

Can HOCs be chained?
	- ✅ Yes. You can nest HOCs to layer multiple behaviors.
	const Enhanced = withTheme(withLogger(MyComponent));

How is HOC different from Render Props or Hooks?
	- HOCs wrap components.
	- Render Props pass functions via props.
	- Hooks allow logic reuse inside function components.
	- Hooks are now preferred, but HOCs are still used in libraries.

🧠 Key Takeaways:

	- HOC = function that returns a new component.
	- Used to add logic to existing components without modifying them.
	- Follows the principle: Component In, Component Out.
	- Helps keep components clean and focused on UI.


7. State Management in React

✅ What is State?
	- State is data that changes over time inside a component.
	- It's managed using the useState hook (or this.state in class components).
	- When state updates, the component re-renders.

	const [count, setCount] = useState(0);
	
✅ What are Props?
	- Props (properties) are read-only data passed from parent to child components.
	- They are used to send data or functions between components.

	```bash
	function Greeting({ name }) {
	return <p>Hello, {name}!</p>;
	}
	```
	
🆚 Difference: State vs Props

| Feature	| State				| Props
|---------------|-------------------------------|-------------------------------|
| Ownership	| Managed inside component	| Passed from parent component  |
| Mutability	| Can be changed using hooks	| Read-only                     |
| Usage		| Track internal changes	| Send data to child components |
| Re-render	| Yes, causes re-render		| Only when changed by parent   |

🧵 What is Props Drilling?

	- Props drilling is when you pass props through many layers of components, even if only the bottom component needs the data.
	- This makes code hard to maintain and deeply nested.

	Example:
	```bash
	<App>
	<Parent>
		<Child>
		<GrandChild someData={data} />
		</Child>
	</Parent>
	</App>
	```
	
	Here, someData is passed through all levels just to reach GrandChild.

🧰 How to Solve Props Drilling?
✅ Use React Context API.

React Context API
✅ What is Context?
Context provides a way to share state or data globally without passing props manually at every level.

🏗️ How to Create and Use Context
1. Create the Context:

	```bash
	import React, { createContext } from 'react';

	const UserContext = createContext();
	export default UserContext;
	```
	
2. Provide Context (wrap your app or part of it):

	```bash
	import UserContext from './UserContext';

	function App() {
	const user = "John";

	return (
		<UserContext.Provider value={user}>
		<Dashboard />
		</UserContext.Provider>
	);
	}
	```
	
3. Use Context in any child component:

	```bash
	import React, { useContext } from 'react';
	import UserContext from './UserContext';

	function Dashboard() {
	const user = useContext(UserContext);
	return <h1>Welcome, {user}</h1>;
	}
	```
	
🧠 When to Use Context?

	Use Context when:
	- You have global data like user, theme, language, settings, auth.
	- You want to avoid props drilling.
	- Multiple components need access to the same data.

⚠️ When not to use Context:

	- For frequently changing values like form input or animation (it may cause re-renders).
	- In very small apps — can overcomplicate simple state flows.

🤔 Common Interview Questions:

What is state and how is it different from props?
→ State is local and mutable. Props are external and read-only.

What is props drilling and how do you solve it?
→ Passing props through many levels. Solved using React Context or libraries like Redux/Zustand.

How does React Context work?
→ Create → Provide → Consume using useContext.

Can we use multiple contexts?
→ ✅ Yes, you can nest multiple contexts if needed.

Is context a state management tool?
→ Yes, it helps manage state globally, but it's basic. For complex apps, people use Redux, Zustand, or Recoil.

🧩 Key Takeaways:
	- State: Local to the component.
	- Props: Passed from parent → child.
	- Props Drilling: Problem when too many levels pass props.
	- Context API: Solution to share data globally without drilling.


8. Redux – State Management Library

✅ What is Redux?
	- Redux is a state management library for JavaScript apps (commonly used with React).
	- It stores the entire app’s state in a single global object (called the store).
	- Components can access or update this store using special functions.

✅ Why Use Redux?
	- To manage global state across multiple components.
	- To avoid props drilling and state duplication.
	- Useful in large applications where state sharing between components is complex.

✅ When to Use Redux?
	Use Redux when:
	- Your app has a lot of shared/global state.
	- You are passing state through many layers of components.
	- You need predictable and centralized state updates (good for debugging).

	Don't use Redux when:
	- Your app is small and simple.
	- You can manage state easily with useState or useContext.

🧱 Core Concepts of Redux

Term		Meaning
Store	 	Holds the global state
Action	 	An object that describes an event/change
Reducer	 	A function that updates the state based on action
Dispatch	Sends an action to the reducer to update state
useSelector	Access state from the Redux store in a component
useDispatch	Send actions from a component to change state

🔧 How Redux Works (Simple Flow):

	Component → dispatch(action) → reducer → store → UI re-renders
	
📦 Example: Redux Counter App (Simple)

1. Install Redux and React-Redux
	```bash
	npm install redux react-redux
	```
	
2. Create Action

	```bash
	// actions.js
	export const increment = () => ({ type: 'INCREMENT' });
	export const decrement = () => ({ type: 'DECREMENT' });
	```
	
3. Create Reducer

	```bash
	// reducer.js
	const initialState = { count: 0 };

	function counterReducer(state = initialState, action) {
	switch (action.type) {
		case 'INCREMENT':
		return { count: state.count + 1 };
		case 'DECREMENT':
		return { count: state.count - 1 };
		default:
		return state;
	}
	}

	export default counterReducer;
	```
	
4. Create Store

	```bash
	// store.js
	import { createStore } from 'redux';
	import counterReducer from './reducer';

	const store = createStore(counterReducer);
	export default store;
	```
	
5. Provide Store to App

	```bash
	// index.js
	import React from 'react';
	import ReactDOM from 'react-dom';
	import { Provider } from 'react-redux';
	import store from './store';
	import App from './App';

	ReactDOM.render(
	<Provider store={store}>
		<App />
	</Provider>,
	document.getElementById('root')
	);
	```
	
6. Use Redux in Component

	```bash
	// App.js
	import React from 'react';
	import { useSelector, useDispatch } from 'react-redux';
	import { increment, decrement } from './actions';

	function App() {
	const count = useSelector(state => state.count);
	const dispatch = useDispatch();

	return (
		<div>
		<h2>Count: {count}</h2>
		<button onClick={() => dispatch(increment())}>+</button>
		<button onClick={() => dispatch(decrement())}>-</button>
		</div>
	);
	}

	export default App;
	```
	
✅ Summary of Redux Flow:
	- Dispatch an action from UI
	- Action goes to Reducer
	- Reducer updates the state
	- Updated state triggers UI re-render via useSelector

🧠 Common Interview Questions for Redux:

What is Redux and why do we use it?
	- Redux is a global state manager used to share state across components and manage complex state logic.

What are the main parts of Redux?
	- Store, Action, Reducer, Dispatch.

What is the use of useSelector and useDispatch?
	- useSelector: to access state
	- useDispatch: to send actions

Can Redux be used with class components?
	- Yes, using connect() and mapStateToProps.

What is middleware in Redux?
	- Middleware like redux-thunk or redux-saga lets you handle async actions (e.g., API calls).

Redux vs Context API?
Feature		Redux						Context API
Complexity	More powerful, more setup	Simple for small apps
Performance	Better with large state		Not optimized for frequent updates
Async		Middleware support			No built-in support

✅ Key Takeaways:

	- Redux is used for predictable, centralized state management.
	- Best for large apps or when multiple components share complex state.
	- Use useSelector, useDispatch in function components.
	- Don't use Redux for small apps — Context or useState is simpler.



9. SSR vs CSR (Server-Side Rendering vs Client-Side Rendering)

✅ What is CSR (Client-Side Rendering)?
	- In Client-Side Rendering, the browser downloads a blank HTML page and a JavaScript bundle.
	- The JavaScript runs in the browser and renders the content on the client side.
	- React apps created with create-react-app use CSR by default.

🧾 CSR Flow:
	- Browser loads basic HTML.
	- Downloads JS bundle.
	- React takes over and renders the UI.
	- Content appears after JavaScript finishes.

✅ Pros of CSR:
	- Fast page transitions after the app loads.
	- Great for dynamic apps (e.g., dashboards, SPAs).
	- Less load on the server.

❌ Cons of CSR:
	- Slower first load, especially on slow networks.
	- Poor SEO (search engines may not index JS-rendered content well).
	- Blank screen until JS loads (bad for performance and accessibility).

✅ What is SSR (Server-Side Rendering)?
	- In Server-Side Rendering, HTML is generated on the server for each request.
	- The client gets a fully-rendered HTML page, and then JavaScript takes over for interactivity.
	- Next.js is a React framework that supports SSR out of the box.

🧾 SSR Flow:
	- User requests a page.
	- Server renders the React components into HTML.
	- Sends the full HTML to the browser.
	- Browser displays content immediately.	- 
	- JavaScript hydrates the page (adds interactivity).

✅ Pros of SSR:
	- Faster initial page load (better for performance and UX).
	- Great for SEO – HTML content is already present.
	- Ideal for content-heavy websites (blogs, e-commerce, etc.).

❌ Cons of SSR:
	- Slower for dynamic data-heavy apps.
	- Higher server load (since it renders HTML for every request).
	- Slightly more complex to set up and maintain.

🆚 SSR vs CSR – Quick Comparison

Feature				CSR (Client-Side)	SSR (Server-Side)
First Load Speed	Slower				Faster
SEO Support			Poor				Excellent
Server Load			Low					High
Setup				Easy (CRA)			Needs SSR-ready framework (Next.js)
Interactivity		After JS loads		After hydration
Use Case		Dashboards, SPAs		Blogs, E-commerce, News sites

🤔 Common Interview Questions:

What is the difference between SSR and CSR?
	- CSR renders everything in the browser.
	- SSR renders HTML on the server and sends it to the client.

Which is better for SEO and why?
	- SSR, because the content is already rendered as HTML when the page is loaded.

What is hydration in SSR?
	- After HTML is rendered on the server and sent to the browser, React takes over and attaches event handlers – this is called hydration.

Which React tools/frameworks support SSR?
	- Next.js is the most popular React framework with built-in SSR support.

Can we combine SSR and CSR?
	- ✅ Yes. You can SSR the initial page and load dynamic content with CSR after that.

🧠 Key Takeaways:

	- CSR: Renders in browser. Best for apps with lots of interactivity and less concern for SEO.
	- SSR: Renders on server. Best for SEO, performance, and content-rich sites.
	- Use Next.js for SSR in React.


10. React Routing, RBAC, and Challenges

1. Routing in React
	- Routing: Allows navigation between different views or pages in a React app.
	- React Router: The most common library used to handle routing in React apps.

Types of Routing

1. Client-Side Routing (CSR):
	- React Router manipulates the URL and renders components accordingly without refreshing the page.
	- Faster as only components are re-rendered.

2. Server-Side Routing (SSR):
	- The server handles routing, and the entire page is loaded each time.
	- Slower than CSR, but useful for SEO and initial page load.

	Basic Routing Setup (React Router)

	```bash
	import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';

	function App() {
	return (
		<Router>
		<Switch>
			<Route path="/" exact component={Home} />
			<Route path="/about" component={About} />
		</Switch>
		</Router>
	);
	}
	```
	
2. Role-Based Access Control (RBAC) with Routing

	- RBAC: Controls access to routes based on the user's role (e.g., admin, user, etc.).
	- How RBAC works with Routing:
		- Only allow users with specific roles to access certain routes (e.g., /admin should only be accessible to users with the "admin" role).

	Example:

	```bash
	<Route path="/admin" render={() => (
	userRole === 'admin' ? <AdminPage /> : <Redirect to="/login" />
	)} />
	```
	
3. Common Challenges in React Routing

1. Route Protection & Authentication

	- Challenge: Prevent unauthorized users from accessing certain routes (e.g., user not logged in).
	- Solution: Create ProtectedRoute components that check if the user is authenticated before rendering the route.

	Example:

	<Route path="/protected" element={isAuthenticated ? <ProtectedPage /> : <Redirect to="/login" />} />
	
2. Role-Based Access Control (RBAC)
	- Challenge: Restrict access to routes based on user roles (e.g., only admin can access /admin).
	- Solution: Use conditional rendering in routes or create wrapper components to handle the role-based restrictions.

	Example:

	<Route path="/admin" element={userRole === 'admin' ? <AdminPage /> : <Redirect to="/login" />} />
	
3. Deep Linking & Refresh Issues
	- Challenge: Refreshing at a deep URL (e.g., /dashboard/settings) can result in a 404 error.
	- Solution: Ensure the server handles all routes by serving index.html for non-static routes (especially in SPA setups).

4. Dynamic Routing
	- Challenge: Handling dynamic routes like /user/:id.
	- Solution: Use useParams() to extract dynamic parameters and load content based on them.

	const { id } = useParams();
	
5. Nested Routing
	- Challenge: Managing nested routes can become cumbersome.
	- Solution: Use Outlet (React Router v6) to render child routes in parent routes.

6. Performance / Code Splitting
	- Challenge: The entire app is bundled into one large JS file, causing slower page load times.
	- Solution: Use React.lazy() with Suspense to load components only when needed.

7. SEO & Crawling Issues (CSR)
	- Challenge: In Client-Side Rendering, the content is not visible to search engines (SEO problem).
	- Solution: Implement SSR (Server-Side Rendering), or use pre-rendering tools like Next.js to allow SEO indexing.

8. Breadcrumbs / Navigation Logic
	- Challenge: Managing dynamic breadcrumbs for deeply nested routes.
	- Solution: Maintain a centralized route configuration to handle breadcrumbs.

9. Maintaining Route Configuration
	- Challenge: Managing a large number of routes becomes repetitive.
	- Solution: Use a centralized route configuration (array or object) to manage and scale routes efficiently.

10. Transition Animations
	- Challenge: Smoothly animating between route transitions.
	- Solution: Use libraries like Framer Motion for route change animations.

Summary of Key Challenges

Challenge						Example Problem								Solution
Route Protection	        	Unauthorized users accessing routes			Use ProtectedRoute or Redirect
Role-Based Access Control		Only admin should access /admin				Check user role before rendering
Deep Linking & Refresh	    	404 when refreshing on deep URLs			Configure server to handle all routes
Dynamic Routing					Routes with dynamic parameters (/user/:id)	Use useParams()
Nested Routing					Handling deeply nested routes				Use Outlet for child routes
Performance / Code Splitting	Slow load times due to large JS files		Use React.lazy() and Suspense
SEO & Crawling					Content not indexed by search engines		Use SSR or static pre-rendering
Breadcrumbs / Navigation		Dynamic breadcrumbs for nested routes		Centralized route configuration
Route Configuration				Managing many routes						Use centralized configuration
Transition Animations			Animating between routes					Use Framer Motion or CSS transitions

React Interview Questions: Routing, RBAC, and Challenges

1. React Routing

What is React Router?
	- React Router is a library used to handle routing in React applications. It allows navigation between different views or pages without refreshing the browser.

What is the difference between Client-Side Routing (CSR) and Server-Side Routing (SSR)?
	- CSR: React Router handles routing in the browser. Faster but not great for SEO.
	- SSR: The server handles routing and sends a fully-rendered page on each request. Better for SEO.

How do you create routes in React?
	- You can create routes using <Route> and wrap your app with <Router>. Here's a basic example:

	```bash
	import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';

	function App() {
	return (
		<Router>
		<Switch>
			<Route path="/" exact component={Home} />
			<Route path="/about" component={About} />
		</Switch>
		</Router>
	);
	}
	```

What is useParams() in React Router?
	- useParams() is a hook that returns the dynamic parameters from the URL, such as id in a URL like /user/:id.

What is the Switch component used for in React Router?
	- The Switch component ensures that only the first matching <Route> is rendered. It wraps multiple routes to ensure only one route is active at a time.
	
2. Role-Based Access Control (RBAC)
What is RBAC (Role-Based Access Control)?
	- RBAC is a method of restricting access to routes or features based on a user's role (admin, user, etc.). In React, this is often used to manage permissions for different user types.

How would you implement RBAC in React Routing?
	- You can create a PrivateRoute or ProtectedRoute that checks the user’s role before rendering a route. If the user doesn’t have permission, they are redirected to a login or unauthorized page.

	```bash
	const ProtectedRoute = ({ role, allowedRole, children }) => {
	return role === allowedRole ? children : <Redirect to="/login" />;
	};
	```
	
Can you give an example of a Route protection for admin users?
	- Here’s an example of restricting access to a route based on the user's role:

	```bash
	<Route path="/admin" render={() => (
	userRole === 'admin' ? <AdminPage /> : <Redirect to="/login" />
	)} />
	```
	
Why is RBAC important in React apps?
	- It ensures that sensitive or restricted pages (like admin dashboards) are accessible only to authorized users, protecting application data and security.

3. React Routing Challenges
What are the challenges of handling route protection in React?
	- Preventing unauthenticated users from accessing private routes.
	- Solution: Use PrivateRoute components that redirect users based on authentication status.

What is the challenge with refreshing deep URLs (like /dashboard/settings)?
	- If you refresh on a deep URL, the browser may show a 404 error because the server doesn’t know how to handle client-side routes.
	- Solution: Configure the server to return index.html for all routes in single-page applications (SPA).

How do you manage deeply nested routes in React?
	- Deeply nested routes can be handled using <Route> components, or with Outlet in React Router v6 for better nested route management.

	Example:

	```bash
	<Route path="/admin" element={<AdminLayout />}>
	<Route path="settings" element={<SettingsPage />} />
	</Route>
	```
	
How do you implement dynamic routes in React?
	- You can implement dynamic routes by using URL parameters (e.g., /user/:id), and then extract parameters using the useParams() hook.

	```bash
	const { id } = useParams();
	```
	
What are the challenges related to performance when dealing with routing?
	- The large initial bundle size can slow down loading time.
	- Solution: Use React.lazy() and Suspense for code splitting, loading only the necessary components on-demand.

What is the issue with SEO and routing in CSR (Client-Side Rendering)?
	- CSR routes may not be indexed by search engines, resulting in poor SEO.
	- Solution: Implement SSR (Server-Side Rendering), or use tools like Next.js for SEO-friendly routes.

What is the challenge with route transitions and animations?
	- Smoothly animating transitions between pages can be tricky.
	- Solution: Use libraries like Framer Motion or CSS transitions to animate route changes.

How do you prevent users from accessing routes after they log out?
	- Ensure that after logout, the user is redirected to the login page or unauthorized route.
	- Solution: Use PrivateRoute to redirect users based on authentication status.

	
11. Async Tasks

1. What are Asynchronous Tasks in React?
	- Asynchronous tasks are tasks that run in the background and do not block the main thread of execution. This is especially important for operations like API calls, setTimeout, event listeners, or reading files.
	- In React, asynchronous tasks are crucial because they allow components to fetch data, handle user input, and interact with APIs without blocking the user interface.

2. How to Handle Async Tasks in React?
	In React, asynchronous tasks are usually handled using Promises, async/await, or in some cases, using state management libraries like Redux for managing side effects.

	Common Ways to Handle Async Operations:
	- Promises:

	You can use Promises to handle asynchronous tasks like fetching data from an API.

	```bash
	useEffect(() => {
	fetch('https://api.example.com/data')
		.then(response => response.json())
		.then(data => setData(data))
		.catch(error => console.error('Error:', error));
	}, []);
	```
	
	- Async/Await:

	async/await makes it easier to handle asynchronous code and looks more like synchronous code. It improves readability and error handling.

	```bash
	import { useState, useEffect } from 'react';
	function DataFetcher() {
	const [data, setData] = useState(null);
	const [loading, setLoading] = useState(true);
	const [error, setError] = useState(null);

	useEffect(() => {
		const fetchData = async () => {
		try {
			const response = await fetch('https://api.example.com/data');
			const result = await response.json();
			setData(result);
		} catch (error) {
			setError(error);
		} finally {
			setLoading(false);
		}
		};

		fetchData();
	}, []);

	if (loading) return <div>Loading...</div>;
	if (error) return <div>Error: {error.message}</div>;
	return <div>{JSON.stringify(data)}</div>;
	}

	export default DataFetcher;
	```
	
3. What is useEffect for Async Operations?
	- useEffect() is often used for asynchronous tasks in React.
	- It is used to trigger API calls or perform other side-effects when the component mounts or updates.
	- By default, useEffect() runs after the render. This means you can place your asynchronous tasks in it, such as API calls, and update the state accordingly.

4. How to Handle Multiple Async Operations in React?
	- There are cases where you need to handle multiple asynchronous operations simultaneously, such as fetching data from multiple sources. You can achieve this with Promise.all() or async/await.

	Example with Promise.all():

	```bash
	import { useState, useEffect } from 'react';
	function MultipleAPIFetch() {
	const [data, setData] = useState(null);
	const [error, setError] = useState(null);

	useEffect(() => {
		const fetchData = async () => {
		try {
			const [res1, res2] = await Promise.all([
			fetch('https://api.example1.com/data'),
			fetch('https://api.example2.com/data'),
			]);
			const data1 = await res1.json();
			const data2 = await res2.json();
			setData([data1, data2]);
		} catch (error) {
			setError(error);
		}
		};

		fetchData();
	}, []);

	if (error) return <div>Error: {error.message}</div>;
	return <div>{JSON.stringify(data)}</div>;
	}

	export default MultipleAPIFetch;
	```
	
5. Handling Loading States and Error States in Async Tasks
	When performing asynchronous operations, it’s important to handle loading states and errors. Here’s how you can handle them in React:

	- Loading State: Show a loading spinner or a message while the asynchronous task is in progress.
	- Error State: Show a meaningful error message if the API request fails.

	```bash
	import { useState, useEffect } from 'react';

	function AsyncComponent() {
	const [data, setData] = useState(null);
	const [loading, setLoading] = useState(true);
	const [error, setError] = useState(null);

	useEffect(() => {
		const fetchData = async () => {
		try {
			setLoading(true);
			const response = await fetch('https://api.example.com/data');
			const result = await response.json();
			setData(result);
		} catch (err) {
			setError('Failed to fetch data');
		} finally {
			setLoading(false);
		}
		};

		fetchData();
	}, []);

	if (loading) return <div>Loading...</div>;
	if (error) return <div>{error}</div>;
	return <div>{JSON.stringify(data)}</div>;
	}

	export default AsyncComponent;
	```
	
6. Error Boundaries for Async Operations
	- React allows you to handle errors during rendering, in lifecycle methods, and in constructors of the whole tree using Error Boundaries.
	- An Error Boundary is a higher-order component that catches JavaScript errors anywhere in a component tree, logs those errors, and displays a fallback UI instead of crashing the component tree.

	Example of an Error Boundary:

	```bash
	class ErrorBoundary extends React.Component {
	constructor(props) {
		super(props);
		this.state = { hasError: false };
	}

	static getDerivedStateFromError(error) {
		return { hasError: true };
	}

	componentDidCatch(error, errorInfo) {
		console.log(error, errorInfo);
	}

	render() {
		if (this.state.hasError) {
		return <h1>Something went wrong!</h1>;
		}

		return this.props.children;
	}
	}

	// Usage:
	<ErrorBoundary>
	<AsyncComponent />
	</ErrorBoundary>
	```
	
7. Common Interview Questions on Async Tasks in React

Question													Answer
What is an async task in React?								Async tasks are tasks like fetching data or performing side-effects in React using Promises or async/await.
How do you fetch data asynchronously in React?				Use the useEffect hook with async/await or then() for promises.
What is useEffect and how does it work with async tasks?	useEffect is a hook that runs after component renders, perfect for async tasks like data fetching.
How do you handle multiple async operations?				Use Promise.all() to handle multiple API calls simultaneously.
What is a loading state in React and how do you handle it?	A loading state indicates that data is being fetched. You can handle it by using a loading state variable.
What is the purpose of Error Boundaries in async tasks?		Error Boundaries are used to catch errors in React components and prevent the app from crashing.


12. Performance Optimization in React

1. Why is Performance Important in React?
	- Performance optimization in React is critical for building fast and responsive applications, especially when dealing with large applications or complex UIs. Poor performance can lead to a sluggish user experience, longer load times, and inefficient resource usage.
	- By optimizing performance, you ensure that your React application runs smoothly even under heavy usage.

2. Techniques for Performance Optimization in React
	- React offers several techniques for optimizing performance. Below are some common methods:

A. React Memoization:
	- React.memo: React provides React.memo to memoize functional components and prevent unnecessary re-renders.
	- When a component is wrapped with React.memo, it will only re-render if its props change. This is useful for functional components that receive the same props multiple times.

	Example:
	'''bash
	import React from 'react';

	const MyComponent = React.memo(({ name }) => {
	console.log('Rendering: ', name);
	return <div>{name}</div>;
	});

	export default MyComponent;
	```
	
When to use: Use React.memo for components that receive static or unchanged props.

B. PureComponent:
	- PureComponent: In class-based components, PureComponent is similar to React.memo. It performs a shallow comparison of props and state, and only re-renders when there are changes.

	Example:
	'''bash
	import React, { PureComponent } from 'react';

	class MyComponent extends PureComponent {
	render() {
		return <div>{this.props.name}</div>;
	}
	}

	export default MyComponent;
	```
	
	When to use: Use PureComponent when you want a class-based component to re-render only when its props or state change.

C. UseCallback and UseMemo Hooks:
	- useCallback: This hook returns a memoized version of a function, preventing unnecessary function re-creations during re-renders.

	'''bash
	import React, { useState, useCallback } from 'react';

	function ParentComponent() {
	const [count, setCount] = useState(0);
  
	const memoizedCallback = useCallback(() => {
		console.log('Callback called');
	}, []);  // Empty dependency array ensures the function is memoized
  
	return (
		<div>
		<button onClick={() => setCount(count + 1)}>Count: {count}</button>
		<ChildComponent onClick={memoizedCallback} />
		</div>
	);
	}

	function ChildComponent({ onClick }) {
	console.log('Rendering ChildComponent');
	return <button onClick={onClick}>Click Me</button>;
	}

	export default ParentComponent;
	```
	
	- useMemo: This hook is used to memoize values that are computationally expensive to avoid recalculating them on every render.

	'''bash
	import React, { useMemo, useState } from 'react';

	function ExpensiveComputationComponent() {
	const [number, setNumber] = useState(0);

	const expensiveCalculation = useMemo(() => {
		console.log('Computing...');
		return number * 1000;  // Simulate expensive operation
	}, [number]);

	return (
		<div>
		<button onClick={() => setNumber(number + 1)}>Increment</button>
		<p>Result: {expensiveCalculation}</p>
		</div>
	);
	}

	export default ExpensiveComputationComponent;
	```
	
When to use:

	- useCallback: To prevent unnecessary re-creation of functions.
	- useMemo: To prevent expensive calculations from re-running unnecessarily.

D. Lazy Loading and Code Splitting:
	- Lazy Loading: Lazy loading involves loading parts of the application only when needed. This reduces the initial load time of the app.
	React.lazy allows you to dynamically import components only when they're required.

	Example:
	'''bash	
	import React, { Suspense, lazy } from 'react';

	const MyComponent = lazy(() => import('./MyComponent'));

	function App() {
	return (
		<Suspense fallback={<div>Loading...</div>}>
		<MyComponent />
		</Suspense>
	);
	}

	export default App;
	```
	
	- Code Splitting: Code splitting allows you to divide your code into smaller chunks. React supports this using React.lazy and React.Suspense.

When to use: Use lazy loading and code splitting for components that are not immediately needed on page load (e.g., modals, routes).

E. Virtualization (Windowing):
	- React Window and React Virtualized are libraries used for rendering only a subset of visible list items to improve performance when rendering large lists or grids. Instead of rendering the entire list at once, these libraries render only the visible portion, which saves resources.

Example:

	'''bash
	import { FixedSizeList as List } from 'react-window';

	function VirtualizedList({ items }) {
	return (
		<List height={150} itemCount={items.length} itemSize={35} width={300}>
		{({ index, style }) => (
			<div style={style}>{items[index]}</div>
		)}
		</List>
	);
	}

	export default VirtualizedList;
	```
	
When to use: Use virtualization for large datasets to optimize performance by only rendering the visible items.

F. Avoiding Inline Functions and Objects:
	- Inline Functions: Each time a component renders, an inline function is created, which can cause unnecessary re-renders of child components.

	// Bad: Inline function
	<ChildComponent onClick={() => doSomething()} />
	
Fix: Define the function outside the JSX or use useCallback to memoize it.

G. Throttling and Debouncing:
	- Throttling and Debouncing are techniques used to limit the rate at which a function is executed. This is especially useful for events like scrolling or typing (e.g., search input) where you don’t want to call a function on every event.

Example of Debouncing (with useEffect and setTimeout):

	'''bash
	import React, { useState, useEffect } from 'react';

	function SearchComponent() {
	const [query, setQuery] = useState('');
	const [debouncedQuery, setDebouncedQuery] = useState('');

	useEffect(() => {
		const timer = setTimeout(() => {
		setDebouncedQuery(query);
		}, 500); // Delay of 500ms

		return () => clearTimeout(timer); // Clean up the timeout on each render
	}, [query]);

	return (
		<div>
		<input 
			type="text" 
			value={query} 
			onChange={(e) => setQuery(e.target.value)} 
			placeholder="Search..."
		/>
		<p>Debounced Query: {debouncedQuery}</p>
		</div>
	);
	}

	export default SearchComponent;
	```
	
H. 🧩 Asset Optimization

🔹 What is Asset Optimization?
	Asset optimization means reducing the size and load time of static assets like:

	- JavaScript bundles
	- CSS files
	- Images
	- Fonts
	- Videos, SVGs, etc.
	
	This is crucial for improving:

	- Initial page load
	- Time to first paint
	- User experience, especially on slower networks

🔹 Common Techniques for Asset Optimization in React

1. Minification & Compression
	Use tools like Webpack, Terser, and UglifyJS to:

	- Minify JS & CSS (remove spaces, comments)
	- Compress files (gzip or Brotli)

	React’s create-react-app does this automatically during production build (npm run build).

2. Code Splitting
	- Split large JS files into smaller chunks.
	- Load only the code needed for the current page.
	- Done using:
		- React.lazy() + Suspense
		- dynamic import() with route-based components

	Example:
	```bash
	const About = React.lazy(() => import('./About'));
	```
	
3. Image Optimization
	- Use .webp or .avif formats (smaller & faster)
	- Lazy load images (e.g., loading="lazy" in <img>)
	- Use CDNs for hosting images
	- Resize images to appropriate dimensions before uploading

4. CSS Optimization
	- Remove unused CSS with PurgeCSS
	- Minify CSS
	- Use CSS modules or CSS-in-JS to scope styles locally
	- Inline critical CSS for faster first render

5. Font Optimization
	- Use modern font formats like WOFF2
	- Only load required font weights/styles
	- Use font-display: swap to avoid blocking render

	Example in CSS:

	'''bash
	@font-face {
	font-display: swap;
	font-family: 'Roboto';
	src: url('Roboto.woff2') format('woff2');
	}
	```
	
6. Lazy Load Non-Critical Assets
	- Delay loading of:
		- Below-the-fold images
		- Third-party scripts (analytics, chat widgets)
	- Load these after the main content has loaded

7. Use a CDN
	- Serve assets from a Content Delivery Network to reduce latency
	- Ensures faster access based on geographic location
	
🧪 Interview Questions on Asset Optimization

Question											Answer
What is asset optimization?							Reducing the size and number of static files like JS, CSS, images to improve performance.
How do you optimize images in React?				Convert to modern formats (WebP), use lazy loading, and resize images.
What is code splitting in React?					Breaking JS bundles into smaller chunks and loading them only when needed.
How do you handle fonts for better performance?		Use modern formats (WOFF2), only load necessary weights, and set font-display: swap.
How does CRA handle asset optimization?				create-react-app minifies, compresses, and splits code during npm run build.

🚀 Final Key Takeaways

Concept				Summary
Memoization			Avoid unnecessary re-renders using React.memo, useMemo, useCallback
Code Splitting		Load only what’s needed with React.lazy()
Virtualization		Render only visible list items
Asset Optimization	Compress and optimize static assets like images, fonts, CSS, and JS
Async Efficiency	Avoid blocking UI, debounce user input, clean up in useEffect
Throttle/Debounce	Optimize frequent events like scroll or input
CDN Usage			Serve files faster based on user location
