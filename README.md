# Practice  :  React Code Snippets          (BEST WAY TO LEARN REACT)

# Question 1
Find the issue
```
import React from "react";
 function App() {
  const items = [
	{ id: 1, text: "Item 1" },
	{ id: 2, text: "Item 2" },
  ];
  const listItems = items.map((item, index) => <li key={index}>{item.text}</li>);
  return <ul>{listItems}</ul>;
}
export default App;
```
Resolved

Explaination : The issue in the code you provided is with the usage of the index as the key prop in the map function. When generating a list of elements in React, each element should have a unique and stable "key" prop assigned to it. Using the index as the key can lead to potential issues with component reordering and performance.

To fix the issue, it's recommended to use a unique identifier from your data instead of the index. In this case, you have an id property for each item, so you can use that as the key.

Here's the modified code with the correct key usage:
```
import React from "react";

function App() {
  const items = [
    { id: 1, text: "Item 1" },
    { id: 2, text: "Item 2" },
  ];

  const listItems = items.map((item) => <li key={item.id}>{item.text}</li>);

  return <ul>{listItems}</ul>;
}

export default App;
```


# Question 2
Find the issue
```
import React, { useMemo } from "react";
 function App() {
  const numbers = [1, 2, 3, 4, 5];
  const doubledNumbers = useMemo(() => numbers.map((n) => n * 2), []);
 return (
	<div>
  	{doubledNumbers.map((number) => (
    	<p key={number}>{number}</p>
  	))}
	</div>
  );
}
 
export default App;
```
Resolved

Explaination : The issue in the provided code regarding the useMemo hook is that the dependency array is empty ([]).

The dependency array in the useMemo hook specifies the dependencies that the memoized value depends on. When any of the dependencies in the array change, the memoized value is recomputed. By providing an empty dependency array, you are telling React that the memoized value (doubledNumbers) should never be recomputed, as there are no dependencies.

However, in this case, the numbers array is used inside the useMemo callback to compute the doubledNumbers array. Since the numbers array is a dependency for the memoized value, it should be included in the dependency array to ensure that the memoized value is updated whenever the numbers array changes.

To fix the issue, you should include the numbers array as a dependency in the dependency array of the useMemo hook:
```
import React, { useMemo } from "react";

function App() {
  const numbers = [1, 2, 3, 4, 5];

  const doubledNumbers = useMemo(() => numbers.map((n) => n * 2), [numbers]);

  return (
    <div>
      {doubledNumbers.map((number) => (
        <p key={number}>{number}</p>
      ))}
    </div>
  );
}

export default App;

```



# Question 3
Find the issue
```
import React, { useCallback, useState } from "react";
function App() {
  const [count, setCount] = useState(0);
 
  const increment = useCallback(() => {
	setCount(count + 1);
  }, []);
   return (
	<div>
  	<button onClick={increment}>Increment</button>
  	<p>Count: {count}</p>
	</div>
  );
}
 
export default App;
```
Resolved
The issue in the code you provided is with the useCallback dependency array. In the current implementation, the dependency array is empty ([]), indicating that the increment function should not have any dependencies. However, the increment function references the count state variable inside its body.

Since the count state variable is a dependency for the increment function, it should be included in the dependency array of the useCallback hook. This ensures that the increment function gets the latest value of count whenever it is invoked.

To fix the issue, you should include [count] as the dependency array for the useCallback hook:
```
import React, { useCallback, useState } from "react";

function App() {
  const [count, setCount] = useState(0);

  const increment = useCallback(() => {
    setCount((prevCount) => prevCount + 1);
  }, [count]);

  return (
    <div>
      <button onClick={increment}>Increment</button>
      <p>Count: {count}</p>
    </div>
  );
}

export default App;

```



# Question 4
Find the issue
```
function TestComponent(props) {
  const [count, setCount] = useState(props.initialCount);
  const handleClick = () => {
    setCount(count + 1);
  };
 return (
	<div>
      <p>Count: {count}</p>
      <button onClick={handleClick}>Increment</button>
    </div>
  );
}
```
Resolved
The issue in the provided code is related to the closure created by the handleClick function that is referencing the initial value of count from the useState hook.

When the component is rendered, the handleClick function is created and captures the initial value of count as a closure. However, subsequent updates to the count state will not affect the captured value inside the handleClick function. Therefore, when the button is clicked, the count state is not properly updated.

To fix this issue, you can use the functional form of the setCount function provided by the useState hook. This allows you to update the state based on its previous value, ensuring that the latest value is used:
```
function TestComponent(props) {
  const [count, setCount] = useState(props.initialCount);
  
  const handleClick = () => {
    setCount((prevCount) => prevCount + 1);
  };
  
  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={handleClick}>Increment</button>
    </div>
  );
}


```



# Question 5
Find the issue
```
import { useState } from "react";
import axios from "axios";
function MyComponent() {
  const [data, setData] = useState([]);
 useEffect(() => {
    axios.get("/api/data").then((response) => {
      setData(response.data);
    });
  }, []);
 
  return <div>{data.map((d) => <p>{d.text}</p>)}</div>;
}
```
Resolved

Using the spread operator when updating state with an array is a best practice to ensure immutability. In the code snippet you provided, using the spread operator is recommended when updating the data state.

Here's the updated code snippet using the spread operator:jsx
```
import { useState } from "react";
import axios from "axios";
function MyComponent() {
  const [data, setData] = useState([]);
 useEffect(() => {
    axios.get("/api/data").then((response) => {
      setData([...response.data]);
    });
  }, []);
 
  return <div>{data.map((d) => <p>{d.text}</p>)}</div>;
}

```




