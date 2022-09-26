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
- [Filtering a list](#challenge-10-2-filtering-a-list)
- [Effects related challenges](#challenge-11-fetch-data-challenges-related-to-effects)
  - [Mini challenge 1](#mini-challenge-1-updating-state-based-on-props-or-state)
  - [Mini challenge 2](#mini-challenge-2-caching-expensive-calculations)
- [Passing pros](#challenge-12-passing-props)
  - [Mini challenge 1](#mini-challenge-1--extract-a-component)

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

<details>
<summary>Code</summary>

```js
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

</details>
<details>
<summary>Solution</summary>

- Add fragment
- Adjust tags

```js
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

</details>

---

### Challenge 2: Display array of users to browser

- First to create a file called `users.js`
- [CodeSandbox](https://codesandbox.io/s/display-an-array-ntpnb0)
- Second to import `users` in `App.js`

> **Note**
>
> If we did not provide an unique key props to `li`, it will show warning like this `Warning: Each child in a list should have a unique "key" prop.`
>
> **Rules of keys**
>
> 1. Must be unique among siblings. However, it’s okay to use the same keys for JSX nodes in different arrays.
>
> 2. Must not change.Don’t generate them while rendering.

<details>
<summary>Code</summary>

```js
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

```js
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

</details>

---

### Challenge 3: Disable Button

- Set initial state as we need to monitor if there's any value.
- use `useState()` to set an initial value.
- [CodeSandbox](https://codesandbox.io/s/disable-submit-btn-9fste3?file=/src/App.js)

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

<details>
<summary>Code</summary>

```js
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

## </details>

### Challenge 4: Two way data binding

- `useState()` to initialize value.
- [CodaSandbox](https://codesandbox.io/s/2-way-data-binding-kyh08q?file=/src/App.js)

<details>
<summary> Code </summary>

```js
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

</details>

---

### Challenge 5: Show text after typing

- `useState()`
- `useEffect()`
- [CodeSandbox](https://codesandbox.io/s/show-value-after-typing-gsbvys)

<details>
<summary> Code </summary>

```js
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

</details>

---

### Challenge 6: Show / hide

- `useState()` to initial state as `true`.
- If `showContent` is `true`, then show content, otherwise, show a smiley face.
- [CodeSandbox](https://codesandbox.io/s/show-hide-2n6ej7?file=/src/App.js)

<details>
<summary> Code </summary>

```js
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

</details>

---

### Challenge 7: Adding to an array

- First to initialize state for text.
- Second to initialize an empty array as we will be adding text inside it.
- Use speard operator instead of `push()` to add a todo.

> **Note**
>
> - Even an array is mutable, we better treat them as immutable when we store in state.
> - **Treat array in React as read-only**, meaning that we shouldn't assign an item inside an array or use methods like `pop()` or `push()`.

<details>
<summary> Code </summary>

```js
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

</details>

---

### Challenge 8: Deleting item from an array

- `filter()` creates a shadow copy of portion of a given array, filtered down to just the elements from the given array that pass the test implemented by the provided function.
- We use `filter()` instead of `splice()` because `filter()` returns a new array, and it won't change the origin one.
- [CodeSandbox](https://codesandbox.io/s/removing-item-from-an-array-0k9jee?file=/src/App.js)

<details>
<summary> Code </summary>

```js
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

</details>

---

### Challenge 9: Accordion Part 1

- feature: User can click `button` to show content.
- What kind of component do we need?
  - `Accordion.js` as parent component that can contain children component and pass data.
  - `Panel.js` as child component, here we display data passed from parent component.
    - Here we will add a button so that user can click for showing content.
- [CodeSanbox](https://codesandbox.io/s/accordion-part-1-0syiz2?file=/src/Panel.js)
- In this challenge, panels are independent, you won't be seeing they both show in the same time when clicking the `show` button.
- Next, we will need to tweak `Accordion` a bit as we want the only one panel is expanded at any given time, and the other one will be hidden.

<details>
<summary> Code </summary>

```js
// App.js
import Accordion from "./Accordion";

export default function App() {
  return <Accordion />;
}
```

```js
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

```js
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

</details>

---

### Challenge 10: Accordion Part 2 (Lifting state)

- In last challenge, we managed to create an `Accordion`, but there's one thing we could tweak for better experience.
- We want one panel expend and the other one close at same time.
- The way to implement this is to make parent component `Accordion.js` controls data.
- In this challenge, we need same components as last one, but adding more to the parent as parent component needs to control which panel is opend.
- [CodeSandbox](https://codesandbox.io/s/accordion-part-2-lifting-state-p4cptu?file=/src/Panel.js)

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

<details>
<summary> Code </summary>

```js
// App.js
import Accordion from "./Accordion";

export default function App() {
  return <Accordion />;
}
```

```js
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

```js
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

</details>

---

### Challenge 10-1: Synced inputs

- This challenge is from [beta reactjs org](https://beta.reactjs.org/learn/sharing-state-between-components#lifting-state-up-by-example)

<details>
<summary>Original code</summary>

```js
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

```js
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

```js
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

</details>

- The code above won't sync input text as `Input.js` component is an **Uncontrolled component**, it has local state of `inputTxt` and the event `onChange`, it can only affect one component instead of both.

- Let's move local state and event from child component to parent component so that parent component can control the behaviour.

<details>
<summary> Solution </summary>

```js
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

```js
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

</details>

---

### Challenge 10-2: Filtering a list

- This challenge is from [beta reactjs org](https://beta.reactjs.org/learn/sharing-state-between-components#lifting-state-up-by-example)
- Feature: Filter out the result that matches user input (whether is uppercase or lowercase, and it will show up while typing.)
- In this challenge, we will need:
  - A file contains data - `data.js`.
  - `SearchBar.js` as input field.
  - `List.js` to list out all contents from `data.js`.
  - `FilterableList.js` as parent component that contains two children above.
  - A way(functionality) of helping us to filter item.


<details>
<summary> Original Code </summary>

```js
// data.js
export const foods = [
  {
    id: 0,
    name: "Sushi",
    description:
      "Sushi is a traditional Japanese dish of prepared vinegared rice",
  },
  {
    id: 1,
    name: "Dal",
    description:
      "The most common way of preparing dal is in the form of a soup to which onions, tomatoes and various spices may be added",
  },
  {
    id: 2,
    name: "Pierogi",
    description:
      "Pierogi are filled dumplings made by wrapping unleavened dough around a savoury or sweet filling and cooking in boiling water",
  },
  {
    id: 3,
    name: "Shish kebab",
    description:
      "Shish kebab is a popular meal of skewered and grilled cubes of meat.",
  },
  {
    id: 4,
    name: "Dim sum",
    description:
      "Dim sum is a large range of small dishes that Cantonese people traditionally enjoy in restaurants for breakfast and lunch",
  },
];
```

```js
// FilterTableList.js
import List from "./List";
import SearchBar from "./SearchBar";
import { foods } from "./data";

export default function FilterableList() {
  return (
    <>
      <SearchBar />
      <hr />
      <List items={foods} />
    </>
  );
}
```

```js
// List.js
function List({ items }) {
  return (
    <table>
      {items.map((food) => (
        <tr key={food.id}>
          <td>{food.name}</td>
          <td>{food.description}</td>
        </tr>
      ))}
    </table>
  );
}
```

```js
// SearchBar.js

import { useState } from "react";

function SearchBar() {
  const [query, setQuery] = useState("");

  function handleChange(e) {
    setQuery(e.target.value);
  }

  return (
    <label>
      Search: <input value={query} onChange={handleChange} />
    </label>
  );
}
```

</details>

<details>
<summary> Optimize </summary>

```js
// FilterTableList.js
// This is parent component which containt `SearchBar.js` and `List.js`

import SearchBar from "./SearchBar";
import List from "./List";
import { useState } from "react";
import { foods } from "./data"

export default FilterTableList() {
  const [query, setQuery] = useState("")

  //create a function that accept foods and query as parameters
  // This function will be responsible for filtering the result that matches query text.

  const filterItems = (items, query) => {
    // make sure that text will be lowercase.
    query = query.toLowerCase();
    return items.filter((item) => item.name.split(" ").some(word => word.toLowerCase().startsWith(query)))
  }

  const results = filterItems(foods, query);

  const handleChange = (e) => {
    setQuery(e.target.value)
  }

  return (
    <SearchBar title="Seach:" query={query} onChange={handleChange}/>
    <List items={results}/>
  )
}
```

```js
// SearchBar.js

export default SearchBar({title, query, onChange}) {
  return (
    <div>
    <h3> </h3>
    <input
      type="text"
      value={query}
      onChange={handleChange}
    />
    </div>
  )
}
```

```js
// List.js
export default List({items}) {
  return (
    <ul>
      {items.map((item) =>(
        <li key={item.id}>
        <span>{item.name}</span>
        <p>{item.description}</p>
        </li>
      ))}
    </ul>
  )
}
```

</details>

- In code above, we move props from child to parent and make children as "controlled" components.

---

### Challenge 11: Fetch data (challenges related to Effects)

> **Note**
>
> Review: Two common cases in whih we don't need Effects.
>
> **1. We don't Effects to transform data for rendering.**
>
> When we update a component's state, React will [commit](https://beta.reactjs.org/learn/render-and-commit) the changes to the DOM, updating the screen, then React will run Effects, if the Effect also immidiately updates the state, it restarts the whole process from scratch.
>
> We can transform all the data ate the top level of the component without using an Effect, it will automatically re-run whenever props or state change.
>
> **2. We don't need Effects to handle user events**
> Because Effect runs in a early stage, we can't predict user's behaviour, so we can just hanlde user events in the corresponding event handlers.

---

#### Mini challenge 1: Updating state based on props or state

In this mini challenge, try to optimize code from `Original code` to see if there's a better solution.

<details>
<summary> Original Code </summary>

```js
import { useState, useEffect } from "react";

export default function Form() {
  const [firstName, setFirstName] = useState("John");
  const [lastName, setLastName] = useState("Smith");
  const [fullName, setFullName] = useState("");

  useEffect(() => {
    setFullName(firstName + " " + setLastName);
  }, [firstName, setLastName]);
}
```

</details>

<details>
<summary> Optimized Code </summary>

```js
import { useState, useEffect } from "react";

export default function Form() {
  const [firstName, setFirstName] = useState("John");
  const [lastName, setLastName] = useState("Smith");

  const fullName = firstName + " " + lastName;
}
```

</details>

> **Note**
>
> Avoid redundant state: If it can be calculated from the exsiting props or state, don't put it in state, calculate it during rerendering.

---

#### mini challenge 2: Caching expensive calculations

In this mini challenge, try to optimize code from `Original code` to see if there's a better solution.

<details>
<summary> Original Code </summary>

```js
import { useState, useEffect } from "react";

export default function TodoList({ todos, filter }) {
  const [newTodo, setNewTodo] = useState("");

  const [visibleTodos, setVisibleTodos] = useState([]);
  useEffect(() => {
    setVisibleTodos(getFilteredTodos(todos, filter));
  }, [todos, filter]);

  // ...
}
```

</details>

<details>
<summary> Optimized Code </summary>

```js
import { useState, useEffect } from "react";

export default function TodoList({ todos, filter }) {
  const [newTodo, setNewTodo] = useState("");

  const visibleTodos = getFilteredTodos(todos, filter);

  // ...
}
```

</details>

> **Note**
>
> If we have a lot of todos, and it slow down `getFilteredTodos()` or vise versa, the `getFilteredTodos()` is already slow, but we do not want to re-render everything, in this case, we can use `useMemo()` to cache / memoize the value (`todos` || `filter`), if they haven't changed, it won't trigger re-render.

<details>
<summary> useMemo to memoize the value</summary>

```js
import { useState, useEffect } from "react";

export default function TodoList({ todos, filter }) {
  const [newTodo, setNewTodo] = useState("");

  const visibleTodos = useMemo(
    () => getFilteredTodos(todos, filter),
    [todos, filter]
  );

  // ...
}
```

</details>

> **Note**
>
> `useMemo` will remember the value of `getFilteredTodos()` during the initial render, for the next render, it will check if `todos` or `filter` are different, if the values weren't changes, `useMemo` will return the last result; if either of them have changed, `useMemo` will call the wrapped function again and store that result instead.

> **Note** **Important**
>
> The function we wrap in `useMemo` runs during rendering, this only works for [pure calculations](https://beta.reactjs.org/learn/keeping-components-pure)
>
> **Purity: Component as formulas**
>
> A pure function is a function with the following characteristics:
>
> 1. **Minds its own business.** It does not change any objects or variables that existed before it was called.
>
> 2. **Same inputs, same outputs**. Given the same inputs, a pure function should always return the same result.

---
### Challenge 12: passing props
[React Beta Challenge](https://beta.reactjs.org/learn/passing-props-to-a-component)

#### mini-challenge 1 : Extract a component

This `Gallery` component contains some very similar markup for two profiles. Extract a `Profile` component out of it to reduce the duplication. You’ll need to choose what props to pass to it.

<details>
<summary> Original Code </summary>

```js
import { getImageUrl } from './utils.js';

export default function Gallery() {
  return (
    <div>
      <h1>Notable Scientists</h1>
      <section className="profile">
        <h2>Maria Skłodowska-Curie</h2>
        <img
          className="avatar"
          src={getImageUrl('szV5sdG')}
          alt="Maria Skłodowska-Curie"
          width={70}
          height={70}
        />
        <ul>
          <li>
            <b>Profession: </b> 
            physicist and chemist
          </li>
          <li>
            <b>Awards: 4 </b> 
            (Nobel Prize in Physics, Nobel Prize in Chemistry, Davy Medal, Matteucci Medal)
          </li>
          <li>
            <b>Discovered: </b>
            polonium (element)
          </li>
        </ul>
      </section>
      <section className="profile">
        <h2>Katsuko Saruhashi</h2>
        <img
          className="avatar"
          src={getImageUrl('YfeOqp2')}
          alt="Katsuko Saruhashi"
          width={70}
          height={70}
        />
        <ul>
          <li>
            <b>Profession: </b> 
            geochemist
          </li>
          <li>
            <b>Awards: 2 </b> 
            (Miyake Prize for geochemistry, Tanaka Prize)
          </li>
          <li>
            <b>Discovered: </b>
            a method for measuring carbon dioxide in seawater
          </li>
        </ul>
      </section>
    </div>
  );
}
```
</details>

<details>
<summary>Solution 1</summary>

```js
// Create a js file to store all datas
// profilesData.js
export const profileData = [
  {
    id: "0",
    name: "Maria Skłodowska-Curie",
    profession: "physicist and chemist",
    numOfAwards: "4",
    awardsDestails:
      "Nobel Prize in Physics, Nobel Prize in Chemistry, Davy Medal,Matteucci Medal",
    achievement: "polonium(element)",
    imgId: "szV5sdG"
  },
  {
    id: "2",
    name: "Katsuko Saruhashi",
    profession: "geochemist",
    numOfAwards: "2",
    awardsDestails: "Miyake Prize for geochemistry, Tanaka Prize",
    achievement: "a method for measuring carbon dioxide in seawater",
    imgId: "YfeOqp2"
  }
];
```
```js
// Gallery.jsx
// datas
import { profileData } from "./profileData";
// component
import Profiles from "./Profiles"

export default function Gallery() {
  return (
    <div>
      <Profiles profiles={profiles}/>
    </div>
  )
}
```
```js
// Profiles.jsx
import {getImageUrl} from "./utils.js"
export default function Profiles({ profiles }) {
    return (
    <div>
      <h1>Notable Scientists</h1>
      {profiles &&
        profiles.map((profile) => (
          <section key={profile.name}>
            <h2>{profile.name}</h2>
            <img
              src={getImageUrl(profile.imgId)}
              alt={profile.name}
              width={70}
              height={70}
            />
            <ul>
              <li>
                <b>Profession: </b>
                {profile.profession}
              </li>
              <li>
                <b>Awards: {profile.numOfAwards} 
                </b>
                ({profile.awardsDestails})
              </li>
              <li>
                <b>Discovered: </b>
                {profile.achievement}
              </li>
            </ul>
          </section>
        ))}
    </div>
  );
}
```
</details>

<details>
<summary>Solution 2</summary>

```js
// Create a js file to store all datas
// profilesData.js
export const profileData = [
  {
    id: "0",
    name: "Maria Skłodowska-Curie",
    profession: "physicist and chemist",
    numOfAwards: "4",
    awardsDestails:
      "Nobel Prize in Physics, Nobel Prize in Chemistry, Davy Medal,Matteucci Medal",
    achievement: "polonium(element)",
    imgId: "szV5sdG"
  },
  {
    id: "2",
    name: "Katsuko Saruhashi",
    profession: "geochemist",
    numOfAwards: "2",
    awardsDestails: "Miyake Prize for geochemistry, Tanaka Prize",
    achievement: "a method for measuring carbon dioxide in seawater",
    imgId: "YfeOqp2"
  }
];
```
```js
// Gallery.jsx
// datas
import { profileData } from "./profileData";
import {getImageUrl} from "./utils.js";

export default function Gallery() {
    const profileItem = profiles.map(profile => {
    return (
      <section key={profile.name}>
            <h2>{profile.name}</h2>
            <img
              src={getImageUrl(profile.imgId)}
              alt={profile.name}
              width={70}
              height={70}
            />
            <ul>
              <li>
                <b>Profession: </b>
                {profile.profession}
              </li>
              <li>
                <b>Awards: {profile.numOfAwards}</b>({profile.awardsDestails})
              </li>
              <li>
                <b>Discovered: </b>
                {profile.achievement}
              </li>
            </ul>
          </section>
    )
  })
  return (
    <div>
      {profileItem}
    </div>
  )
}
```
</details>

