# React Best Practices

The React Best Practices Application is a demo project showcasing best practices in React.js development.

## Table of Contents

- [Getting Started](#getting-started)
- [Best Practices](#best-practices)
- [Conclusion](#conclusion)

## Getting Started

The **React Best Practices** is designed to showcase and adhere to the best practices for developing applications using React.js. This project serves as a reference and a learning tool for developers who aim to write clean, maintainable, and scalable React code. The application demonstrates a variety of techniques and patterns that are considered best practices in the React community. You are welcome to make suggestions or corrections if you find any inaccuracies.

## Best Practices

Here is some best practices. Let's get started.

### Use JSX ShortHand

Try to use JSX shorthand for passing boolean variables. Let's say you want to control the title visibility of a Navbar component.

**Bad Practice**

```
const Component = () => {
  <Navbar showTitle={true} />
};
```

**Good Practice**

```
const Component = () => {
  <Navbar showTitle />
};
```

### Short-Circuit evaluation in JSX

**Bad Practice**

```
const Component = () => {
  return isTrue ? <p>Text</p> : null;
};
```

**Good Practice**

```
const Component = () => {
  return isTrue && <p>Text</p>
};
```

### Avoid Overusing Variables

Overusing variables and leaving unused variables in your code can hinder maintenance and readability. It's important to keep your code clean by only declaring variables that you actually use.

**Bad Practice**

```
const calculateTotal = (items) => {
  let total = 0;
  let itemCount = items.length; // Unused variable
  let index = 0; // Unused variable

  for (let i = 0; i < items.length; i++) {
    total += items[i].price;
  }

  let averagePrice = total / items.length; // Unused variable

  return total;
};
```

**Good Practice**

```
const calculateTotal = (items) => {
  let total = 0;

  for (let i = 0; i < items.length; i++) {
    total += items[i].price;
  }

  return total;
}
```

### Use Object Destructuring

When using direct property access with dot notation to access individual properties of an object, it works well for simple cases.

**Bad Practice**

```
const obj = {
   id: 1,
   name: "Morning Task",
};

const id = obj.id;
const name = obj.name;
```

**Good Practice**

```
const obj = {
   id: 1,
   name: "John Smith",
};

const { id, name = "Oliver Jake" } = obj; 
```

### Object Destructuring for Props

Instead of passing the entire props object, use object destructuring to extract the specific prop names to enhance code clarity and makes it clear which values the component is using. This eliminates the need to reference the props object every time you want to access a prop.

**Bad Practice**

```
const Button = (props) => {
  return <button>{props.text}</button>
}
```

**Good Practice**

```
const Button = ({ text }) => {
  return <button>{text}</button>
}
```

### Use Arrow Functions

Benefits of using arrow functions:

- Makes the code more compact and expressive.
- Automatically binds the context, reducing the chances of this-related bugs.
- Improves code maintainability.

**Bad Practice**

```
function sum(a, b) {
  return a + b;
}
```

**Good Practice**

```
const sum = (a, b) => a + b;
```

### Unnecessary Div

When returning a single component, avoid wrapping it in an unnecessary `<div>`.

**Bad Practice**

```
const Button = () => {
  return (
    <div>
      <button>Close</button>
    </div>
  );
};
```

**Good Practice**

```
const Button = () => {
  return (
    <button>Close</button>
  );
};
```

When returning multiple components, use a `<React.Fragment>` or its shorthand form `<>`.

**Bad Practice**

```
const MyComponent = () => {
  return (
    <div>
      <Header />
      <Content />
      <Footer />
    </div>
  );
}
```

**Good Practice**

```
import React from "react";

const MyComponent = () => {
  return (
    <React.Fragment>
      <Header />
      <Content />
      <Footer />
    </React.Fragment>
  );
}
```

With shorthand fragment

```
const MyComponent = () => {
  return (
    <>
      <Header />
      <Content />
      <Footer />
    </>
  );
}
```

### JSX in Parentheses

If your component spans more than one line, always wrap it in parentheses.

**Bad Practice**

```
return <Component variant="long">
        <MyChild />
    </Component>;
```

**Good Practice**

```
return (
    <Component variant="long">
      <MyChild />
    </Component>
);
```

### Prop Naming

Always use camelCase for prop names or PascalCase if the prop value is a React component.

**Bad Practice**

```
<Component
  UserName="hello"
  phone_number={12345678}
/>
```

**Good Practice**

```
<Component
  userName="hello"
  phoneNumber={12345678}
  Component={SomeComponent}
/>
```

### Pass Objects Instead of Basic Data

To reduce the number of props, pass an object containing related data instead of individual values. This method consolidates related information and streamlines future modifications.

**Bad Practice**

```
<BlogPost
  title={post.title}
  author={post.author}
  date={post.date}
  content={post.content}
/>
```

**Good Practice**

```
<BlogPost post={post} />
```

### Default Prop Values

For enhanced readability, define default prop values directly within the function parameters. Avoid segregating default values into a defaultProps property.

**Bad Practice**

```
const Component = (props) => {
  // ...render component
}

Component.defaultProps = {
  theme: "primary",
  label: "Text",
}
```

**Good Practice**

Method 1: default props with destructuring.

```
const Component = (props) => {
  const { theme = "primary", label = "Text", ...restProps } = props;
  // ...render component
}
```

Method 2: default values assigned in the function parameters

```
const Component = ({ theme = "primary", label = "Text", ...restProps }) => {
  // ...render component
}
```

### Self-Closing Tags

In React, when a component has no children, it's advisable to use a single tag closure for clarity. This clearly indicates that the component does not support children.

**Bad Practice**

```
const Component = () => {
  return <Card text="Hello"></Card>
}
```

**Good Practice**

```
const Component = () => {
  return <Card text="Hello" />
}
```

### Components Naming Convention

Use descriptive and meaningful names for React components. Use PascalCase (capitalizing the first letter of each word) for component names. The component's file using PascalCase, matching the component name, example, `TodoItem.tsx`.

**Bad Practice**

```
const todoItem =  () => {
    // render component
};
```

**Good Practice**

```
const TodoItem =  () => {
    // render component
};
```

### State variables

Prefix state variables with is, has, or should to denote boolean values.

**Bad Practice**

```
const [active, setActive] = useState(false);
const [error, setError] = useState(false);
const [render, setRender] = useState(true);
```

**Good Practice**

```
const [isActive, setIsActive] = useState(false);
const [hasError, setHasError] = useState(false);
const [shouldRender, setShouldRender] = useState(true);
```

### Minimize Comments to Essential Points

Limit comments in code to essential points only. This aligns with React best practices and serves two purposes:

- Maintains visual clarity in code.
- Avoids potential conflicts between comments and code when making alterations later on.

### Documenting React Components with JSDoc

JSDoc, a widely-used documentation syntax for JavaScript, can also be utilized in React components to offer comprehensive insights into the component's purpose, props, state, and more. Incorporating JSDoc comments can greatly enhance the developer experience by providing valuable information directly within the code editor.

Below is an example demonstrating how to document a React functional component using JSDoc:

```
/**
 * Represents a user profile component.
 *
 * @component
 * @param {Object} props - The component props.
 * @param {string} props.userName - The name of the user.
 * @param {string} props.bio - The biography of the user.
 * @returns {React.ReactElement} A user profile element.
 */
const UserProfile = ({ userName, bio }) => {
  return (
    <div className="user-profile">
      <h2>{userName}</h2>
      <p>{bio}</p>
    </div>
  );
}
```

### Avoid Using Indexes as Key Props

Using indexes as key props can lead to incorrect rendering, especially when adding, removing, or reordering list items. This can result in poor performance and incorrect component updates.

Using unique and stable identifiers as keys provides several benefits:

- Efficiently update and reorder components in lists.
- Reduce potential rendering issues.
- Avoid incorrect component updates.

**Bad Practice**

```
const renderItem = (todo, index) => {
  const { name } = todo;
  return <li key={index}>{name}</li>;
};
```

**Good Practice**

```
const renderItem = (todo) => {
  const { id, name } = todo;
  return <li key={id}>{name}</li>;
};
```

### Prefer Using Template Literals

Using string concatenation can result in verbose code and make string interpolation or concatenation more difficult.

Benefits of using template literals:

- Simplifies string manipulation by allowing variable interpolation within the string.
- Makes code more expressive and easier to read.
- Supports multi-line strings without additional workarounds.
- Improves code formatting.

**Bad Practice**

```
const userGreeting = (userName, userAge) => {
  return "Hello, " + userName + "! You are " + userAge + " years old.";
};
```

**Good Practice**

```
const userGreeting = (userName, userAge) => {
  return `Hello, ${userName}! You are ${userAge} years old.`;
};
```

### Prefer Implicit Returns in Small Functions

Using explicit returns can make small function definitions unnecessarily longer and harder to read. It may result in more cluttered code due to additional curly braces and return statements.

Benefits of using implicit return:

- Reduces code verbosity.
- Improves code readability.
- Enhances code maintainability by focusing on the main logic rather than return statements.

**Bad Practice**

```
const square = value => {
  return value * value;
}
```

**Good Practice**

```
const square = value => value * value;
```

## Conclusion

Thank you for taking the time to explore these React best practices. By following these guidelines, you can write cleaner, more maintainable, and more efficient React code. We hope you find these tips helpful in your development journey.

Feel free to contribute to this repository by making suggestions or corrections if you find any inaccuracies. Happy coding!
