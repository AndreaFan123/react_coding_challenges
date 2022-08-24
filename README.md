# React Coding Challenges

## Table of Contents

- [Convert some HTML to JSX](#challenge-1--convert-some-html-to-jsx)
- [Display array of users to browser](#challenge-2-display-array-of-users-to-browser)
- [Disable Button](#challenge-3-disable-button)
- [Two way data binding](#challenge-4-two-way-data-binding)
- [Show text ater typing](#challenge-5-show-text-after-typing)
- [Show and Hide](#challenge-6-show--hide)
- [Adding to an array](#challenge-7-adding-to-an-array)
- [Deleting item from an array](#challenge-8-deleting-item-from-an-array)
- [Accordion P1](#challenge-9-accordion-part-1)
- [Accordion P2 (Lifting State)](#challenge-10-accordion-part-2-lifting-state)
- [Synced inputs](#challenge-10-1-synced-inputs)

---

### Challenge 1 : Convert some HTML to JSX

> **Note**
> Review: What is JSX
>
> JSX is a syntax extension for JavaScript that lets you write HTML-like markup inside a JavaScript file.
>
> Rules:
>
> 1. **Return a single root element**
>
> JSX looks like HTML, but under the hood it is transformed into plain JavaScript objects. You can’t return two objects from a function without wrapping them into an array.
>
> 2. **Close all the tags**
>
> JSX requires tags to be explicitly closed: self-closing tags like `<img>` must become `<img />`
>
> 3. **CamelCase most of the things!**

```javascript
export default function Bio() {
  return (
    <div class="intro">
      <h1>Welcome to my website!</h1>
    </div>
    <p class="summary">
      You can find my thoughts here.
      <br><br>
      <b>And <i>pictures</b></i> of scientists!
    </p>
  );
}
```

#### Solution

- Add fragment
- Adjust tags

```javascript
export default function Bio() {
  return (
    <>
      <div class="intro">
        <h1>Welcome to my website!</h1>
      </div>
      <p class="summary">
        You can find my thoughts here.
        <br />
        <br />
        <b>
          {" "}
          And <i>pictures</i>
        </b> of scientists!
      </p>
    </>
  );
}
```

---

### Challenge 2: Display array of users to browser

- First to create a file called `users.js`
- [CodeSandbox](https://codesandbox.io/s/display-an-array-ntpnb0)

```javascript
export const users = [
  {
    name: "John",
    age: 12,
  },
  {
    name: "Alex",
    age: 32,
  },
];
```

- Second to import `users` in `App.js`

```javascript
import "./styles.css";
import { users } from "./users";

export default function App() {
  return (
    <div className="App">
      <h1>User Profiles</h1>
      {users.map((user) => (
        <li key={user.name}>
          {user.name}: {user.age} years old
        </li>
      ))}
    </div>
  );
}
```

> **Note**
>
> If we did not provide an unique key props to `li`, it will show warning like this `Warning: Each child in a list should have a unique "key" prop.`
>
> **Rules of keys**
>
> 1. Must be unique among siblings. However, it’s okay to use the same keys for JSX nodes in different arrays.
>
> 2. Must not change.Don’t generate them while rendering.

---

### Challenge 3: Disable Button

- Set initial state as we need to monitor if there's any value.
- use `useState()` to set an initial value.
- [CodeSandbox](https://codesandbox.io/s/disable-submit-btn-9fste3?file=/src/App.js)

```javascript
import { useState } from "react";
export default function App() {
  // set value
  const [inputTxt, setInputTxt] = useState("");

  const handleChange = (e) => {
    e.preventDefault();
    setInputtxt(e.target.value);
  };

  return (
    <div>
      <input type="text" value={inputTxt} onChange={handleChange} />
      <button disable={inputTxt === ""}>Submit</button>
    </div>
  );
}
```

> **Note**
>
> Review: `useState()`
>
> `useState` is a React Hook that lets you add a state variable to your component.

> **Warning**
>
> Calling the set function does not change the current state in the already executing code, It only affects what useState will return starting from the next render.
>
> [React Docs - useState](https://beta.reactjs.org/apis/react/useState)

---

### Challenge 4: Two way data binding

- `useState()` to initialize value.
- [CodaSandbox](https://codesandbox.io/s/2-way-data-binding-kyh08q?file=/src/App.js)

```javascript
import "./styles.css";
import { useState } from "react";

export default function App() {
  const [txt, setTxt] = useState("");

  const handleChnage = (e) => {
    setTxt(e.target.value);
  };

  return (
    <div className="App">
      <input type="text" value={txt} onChange={handleChnage} />
      <p>{txt}</p>
    </div>
  );
}
```

---

### Challenge 5: Show text after typing

- `useState()`
- `useEffect()`
- [CodeSandbox](https://codesandbox.io/s/show-value-after-typing-gsbvys)

```javascript
import { useState, useEffect } from "react";

export default function App() {
  // initial 2 states
  const [text, setText] = useState("");
  const [showText, setShowText] = useState("");

  // use useEffect() and pass text as dependency
  useEffect(() => {
    const timeoutId = setTimeOut(() => {
      setShowText(text);
    }, 300);

    return () => {
      clearTimeout(timeoutId);
    };
  }, [text]);

  return (
    <div className="App">
      <input
        type="text"
        value={text}
        onChange={(e) => setTxt(e.target.value)}
      />
      <p>{showText}</p>
    </div>
  );
}
```

---

### Challenge 6: Show / hide

- `useState()` to initial state as `true`.
- If `showContent` is `true`, then show content, otherwise, show a smiley face.
- [CodeSandbox](https://codesandbox.io/s/show-hide-2n6ej7?file=/src/App.js)

```javascript
import { useState } from "react";

export default function App() {
  const [showContent, setShowContent] = useState(true);

  const handleClick = () => {
    setShowContent(!showContent);
  };

  return (
    <div>
      <button onClick={handleClick}>
        {showContent ? "Hide Content" : "Show Content"}
      </button>
      {showContent ? <p>Hello, I am here</p> : <p> :) </p>}
    </div>
  );
}
```

---

### Challenge 7: Adding to an array

- First to initialize state for text.
- Second to initialize an empty array as we will be adding text inside it.
- Use speard operator instead of `push()` to add a todo.

```javascript
import { useState } from "react";

export default function App() {
  const [todo, setTodo] = useState("");
  const [todoLists, setTodoLists] = useState([]);

  const handleChange = (e) => {
    setTodo(e.target.value);
  };

  const handleClick = () => {
    // set id = 0
    let id = 0;
    // clear input after adding
    setTodo("");
    setTodoLists([...todoLists, { id: id++, todo: todo }]);
  };

  render(
    <div>
      <input type="text" value={todo} onChange={handleChange} />
      <button onClick={handleClick}>Add</button>
      <ul>
        {todoLists.map((todoList) => (
          <li key={todoList.id}>{todoList.todo}</li>
        ))}
      </ul>
    </div>
  );
}
```

> **Note**
>
> - Even an array is mutable, we better treat them as immutable when we store in state.
> - **Treat array in React as read-only**, meaning that we shouldn't assign an item inside an array or use methods like `pop()` or `push()`.

---

### Challenge 8: Deleting item from an array

- `filter()` creates a shadow copy of portion of a given array, filtered down to just the elements from the given array that pass the test implemented by the provided function.
- We use `filter()` instead of `splice()` because `filter()` returns a new array, and it won't change the origin one.
- [CodeSandbox](https://codesandbox.io/s/removing-item-from-an-array-0k9jee?file=/src/App.js)

```javascript
import "./styles.css";
import { useState } from "react";

export default function App() {
  const [todo, setTodo] = useState("");
  const [todoLists, setTodoLists] = useState([]);

  const handleChange = (e) => {
    setTodo(e.target.value);
  };

  const handleAdd = () => {
    let id = 0;
    setTodo("");
    setTodoLists([...todoLists, { id: id++, todo: todo }]);
  };

  return (
    <div className="App">
      <input type="text" value={todo} onChange={handleChange} />
      <button onClick={handleAdd}>Add</button>
      <ul>
        {todoLists.map((todoList) => (
          <>
            <li key={todoList.id}>{todoList.todo}</li>
            <button
              onClick={() => {
                setTodoLists(todoLists.filter((t) => t.id !== todoList.id));
              }}
            >
              Delete
            </button>
          </>
        ))}
      </ul>
    </div>
  );
}
```

---

### Challenge 9: Accordion Part 1

- feature: User can click `button` to show content.
- What kind of component do we need?
  - `Accordion.js` as parent component that can contain children component and pass data.
  - `Panel.js` as child component, here we display data passed from parent component.
    - Here we will add a button so that user can click for showing content.
- [CodeSanbox](https://codesandbox.io/s/accordion-part-1-0syiz2?file=/src/Panel.js)

```javascript
// App.js
import Accordion from "./Accordion";

export default function App() {
  return <Accordion />;
}
```

```javascript
// Accordion.js
import Panel from "./Panel";

export default function Accordion() {
  return (
      <>
    <Panel title="Story 1">
      Lorem Ipsum is simply dummy text of the printing and typesetting industry.
      Lorem Ipsum has been the industry's standard dummy text ever since the
      1500s
    </Panel>
    <Panel title="Story 2">
      when an unknown printer took a galley of type and scrambled it to make a
      type specimen book. It has survived not only five centuries
    </Panel>
  </>;
  )
}
```

```javascript
// Panel.js
import { useState } from "react";

export default function Panel({title, children}) {
  const [isActive, setIsActive] = useState(false);

  const handleShow = () {
    setIsActive(true);
  }

  return (
    <section>
      <h3>{title}</h3>
      {isActive ? <p>{children}</p> : <button onClick={handleShow}>Show</button>}
    </section>
  )
}
```

- In this challenge, panels are independent, you won't be seeing they both show in the same time when clicking the `show` button.
- Next, we will need to tweak `Accordion` a bit as we want the only one panel is expanded at any given time, and the other one will be hidden.

---

### Challenge 10: Accordion Part 2 (Lifting state)

- In last challenge, we managed to create an `Accordion`, but there's one thing we could tweak for better experience.
- We want one panel expend and the other one close at same time.
- The way to implement this is to make parent component `Accordion.js` controls data.
- In this challenge, we need same components as last one, but adding more to the parent as parent component needs to control which panel is opend.
- [CodeSandbox](https://codesandbox.io/s/accordion-part-2-lifting-state-p4cptu?file=/src/Panel.js)

```javascript
// App.js
import Accordion from "./Accordion";

export default function App() {
  return <Accordion />;
}
```

```javascript
// Accordion.js
import { useState } from "react";

export default Accordion() {
  // initialize active index
  const [activeIndex, setActiveIndex] = useState(0);

  return (
      <>
    <Panel
      title="Story 1"
      isActive={activeIndex === 1}
      onShow={() => setActiveIndex(1)}
      >
      Lorem Ipsum is simply dummy text of the printing and typesetting industry.
      Lorem Ipsum has been the industry's standard dummy text ever since the
      1500s
    </Panel>
    <Panel
      title="Story 2"
      isActive={activeIndex === 0}
      onShow={() => setActiveIndex(0)
      >
      when an unknown printer took a galley of type and scrambled it to make a
      type specimen book. It has survived not only five centuries
    </Panel>
  </>;
  )
}
```

```javascript
// Panel.js
import { useState } from "react";

export default function Panel({ title, children, isActive, onShow }) {
  const [isActive, setIsActive] = useState(false);

  return (
    <section>
      <h3>{title}</h3>
      {isActive ? <p>{children}</p> : <button onClick={onShow}>Show</button>}
    </section>
  );
}
```

> **Note**
>
> **Review : Uncontrolled vs. controlled component**
>
> Usually uncontrolled component is referring to component with local state, for example : `Panel.js` from challenge 9, it controlled the `isActive` state.
>
> Controlled component on the other hand is driven by props rather then its local state, for example: `Panel.js` from challenge 10, it is fully controlled by its parent component.
>
> Generally, uncontrolled component is less flexible eventhough it requires less configuration, hence it's easier to use within parent component; Controlled components are maximally flexible, but they require the parent components to fully configure them with props.
>
> [React: Lifting state](https://beta.reactjs.org/learn/sharing-state-between-components#lifting-state-up-by-example)

---

### Challenge 10-1: Synced inputs

- This challenge is from [beta reactjs org](https://beta.reactjs.org/learn/sharing-state-between-components#lifting-state-up-by-example)

Original code:

```javascript
// App.js
import SyncedInputs from "./SyncedInputs";

export default function App() {
  return (
    <div>
      <SyncedInputs />
    </div>
  );
}
```

```javascript
// SyncedInputs.js

import Input from "./Input";

export default function SyncedInputs() {
  return (
    <>
      <Input label="First Input" />
      <Input label="Second Input" />
    </>
  );
}
```

```javascript
// Input.js

import { useState } from "react";

export default Input({label}){
  const [inputTxt, setInputTxt] = useState("");

  const handleChange = (e) => {
    setInputTxt(e.target.value);
  }

  return (
    <>
    <input
      type="text"
      value={inputTxt}
      onChange={handleChange}
    />
    </>
  )
}
```

- The code above won't sync input text as `Input.js` component is an **Uncontrolled component**, it has local state of `inputTxt` and the event `onChange`, it can only affect one component instead of both.

- Let's move local state and event from child component to parent component so that parent component can control the behaviour.

```javascript
// SyncedInputs.js

import { useState } from "react";
import Input from "./Input";

export default function SyncedInputs() {
  const [inputTxt, setInputTxt] = useState("");

  const handleChange = (e) => {
    setInputTxt(e.target.value);
  };

  return (
    <>
      <Input label="First Input" value={inputTxt} onChange={handleChange} />
      <Input label="Second Input" value={inputTxt} onChange={handleChange} />
    </>
  );
}
```

```javascript
// Input.js

export default function Input({ label, value, onChange }) {
  return (
    <>
      <h3> {label}</h3>
      <input type="text" value={value} onchnage={onChange} />
    </>
  );
}
```

---

### Challenge 10-2: Filtering a list

- Functionality: Filter out the result that matches user input.
- In this challenge, we will need:
  - A file contains data - `data.js`.
  - `SearchBar.js` as input field.
  - `List.js` to list out all contents from `data.js`.
  - `FilterableList.js` as parent component that contains two children above.

Original Code

```javascriptX

```
