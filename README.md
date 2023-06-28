# reactCodeSnippets

# Find the issue 
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

# Resolved
Returned JSX is not wrapped with parent JSX
```
<><ul>{listItems}</ul></>
<Fragment><ul>{listItems}</ul></Fragment>
```

