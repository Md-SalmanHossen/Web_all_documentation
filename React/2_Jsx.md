

---

## 🟩 JSX in React: Complete In-Depth Guide 

---

### 🟢 1. What is JSX?

JSX হচ্ছে JavaScript এর ভিতরে HTML-like syntax use করার একটা special feature। এটা JavaScript এর extension যা React Component তৈরির সময় HTML elements গুলাকে JavaScript এর ভিতরে embed করতে দেয়।

**উদাহরণ:**

```jsx
const element = <h1>Hello, React!</h1>;
```

➡️ JavaScript browser JSX বোঝে না, তাই Babel JSX কে compile করে JavaScript code এ রূপান্তর করে।

**⛳ JSX এর compiled form:**

```jsx
const element = React.createElement("h1", null, "Hello, React!");
```

---

### 🟢 2. JSX এর ব্যবহার কেন?

✅ Code দেখতেও সহজ
✅ HTML ও JavaScript একসাথে লিখা যায়
✅ Component গুলো cleaner ও readable হয়
✅ UI updates দ্রুত বোঝা যায়
✅ JavaScript expressions সহজে handle করা যায়

---

### 🟢 3. JSX এর All Rules & Syntax

#### 🔸 Rule 1: One Parent Element per Return

JSX-তে সবকিছু একটি parent element এর ভিতরে থাকতে হবে।

❌ ভুল:

```jsx
return (
  <h1>Hello</h1>
  <p>World</p>
);
```

✅ ঠিক:

```jsx
return (
  <div>
    <h1>Hello</h1>
    <p>World</p>
  </div>
);
```

✅ React Fragment (<> \</>) use করা যায়:

```jsx
return (
  <>
    <h1>Hello</h1>
    <p>World</p>
  </>
);
```

---

#### 🔸 Rule 2: Use `className` instead of `class`

```jsx
<div className="box">Hello</div>
```

---

#### 🔸 Rule 3: Use camelCase for attributes

```jsx
<button onClick={handleClick}>Click Me</button>
```

---

#### 🔸 Rule 4: Expressions must be inside `{ }`

```jsx
const name = "Salman";
return <h1>Hello, {name}</h1>;
```

✅ Use ternary or logical operators:

```jsx
{isLoggedIn ? <p>Welcome</p> : <p>Please log in</p>}
```

---

#### 🔸 Rule 5: Styles in JSX (Inline)

```jsx
const myStyle = {
  color: "blue",
  fontSize: "20px"
};
return <h1 style={myStyle}>Styled Heading</h1>;
```

---

#### 🔸 Rule 6: Self-Closing Tags must end with `/`

✅ Correct:

```jsx
<img src="logo.png" alt="Logo" />
<input type="text" />
```

---

#### 🔸 Rule 7: Conditional Rendering

✅ Ternary operator:

```jsx
{isLoggedIn ? <p>Dashboard</p> : <p>Login</p>}
```

✅ Logical AND (`&&`):

```jsx
{user && <p>Welcome, {user.name}</p>}
```

---

#### 🔸 Rule 8: Rendering Lists with `map()`

```jsx
const items = ['Apple', 'Banana', 'Mango'];
return (
  <ul>
    {items.map((item, index) => (
      <li key={index}>{item}</li>
    ))}
  </ul>
);
```

---

#### 🔸 Rule 9: Comments in JSX

```jsx
return (
  <div>
    {/* This is a comment */}
    <h1>Hello</h1>
  </div>
);
```

---

#### 🔸 Rule 10: Spread Operator in JSX

```jsx
const props = { name: "Salman", age: 20 };
<Component {...props} />
```

---

### 🟢 4. JSX vs HTML Table Summary:

| HTML       | JSX          |
| ---------- | ------------ |
| `class`    | `className`  |
| `for`      | `htmlFor`    |
| `onclick`  | `onClick`    |
| `style=""` | `style={{}}` |
| `tabindex` | `tabIndex`   |
| `readonly` | `readOnly`   |

---

### 🟢 5. Advanced: JSX Functions Inside JSX

```jsx
function greet(name) {
  return `Hello, ${name}`;
}
return <h2>{greet("Salman")}</h2>;
```

---

### 🟢 6. JSX Best Practices

✅ Use meaningful names
✅ Avoid deeply nested JSX
✅ Extract big JSX to child components
✅ Use `React.Fragment` instead of extra `<div>`
✅ Always use `key` in `.map()`

---

### 🟢 Bonus: JSX Tricks

✅ **Render HTML safely:**

```jsx
<div dangerouslySetInnerHTML={{ __html: "<p>HTML Content</p>" }} />
```

🔒 Use with extreme caution for security!

✅ **Conditional className:**

```jsx
<div className={isActive ? "active" : "inactive"}>Status</div>
```

✅ **Destructuring props:**

```jsx
function Card({ title, description }) {
  return <h1>{title}</h1>;
}
```

---

### 🔚 Summary:

JSX = HTML-like syntax + JavaScript power
It allows React to build powerful, readable UI components efficiently.


---

## 🔸 **Ternary Operator ( ? : ) in JSX**

JSX-এ যদি আমরা কোন condition check করে **if-else** এর মত behavior করতে চাই, তাহলে Ternary Operator ব্যবহার করি।

📌 Syntax:

```jsx
condition ? true_part : false_part
```

➡️ এটা if-else এর মতো কাজ করে।

### ✅ উদাহরণ:

```jsx
const isLoggedIn = true;

return (
  <div>
    {isLoggedIn ? <p>Welcome Back!</p> : <p>Please Log In</p>}
  </div>
);
```

**ব্যাখ্যা:**

* যদি `isLoggedIn === true`, তাহলে `<p>Welcome Back!</p>` render হবে (👉 **if part**)
* না হলে `<p>Please Log In</p>` render হবে (👉 **else part**)

---

## 🔸 **Logical AND (&&) Operator in JSX**

Logical `&&` operator শুধুমাত্র **if** এর মত কাজ করে — মানে শুধু **true হলে** কোনো JSX render করবে।

📌 Syntax:

```jsx
condition && JSX
```

➡️ এটি short-circuit করে — যদি condition false হয়, JSX render হয় না।

### ✅ উদাহরণ:

```jsx
const isAdmin = true;

return (
  <div>
    {isAdmin && <p>Welcome, Admin!</p>}
  </div>
);
```

**ব্যাখ্যা:**

* যদি `isAdmin === true`, তাহলে `<p>Welcome, Admin!</p>` render হবে (**if part only**)
* যদি `isAdmin === false`, তাহলে কিছুই render হবে না (**no else part**)

---

## 🔁 Summary Table:

| Operator            | Condition true হলে | Condition false হলে |
| ------------------- | ------------------ | ------------------- |
| `condition ? a : b` | `a` render হবে     | `b` render হবে      |
| `condition && a`    | `a` render হবে     | কিছুই render হবে না |

---

## 🎯 Bonus Example (Both Used):

```jsx
const isLoggedIn = true;
const hasMessages = true;

return (
  <div>
    {/* Ternary Operator */}
    {isLoggedIn ? <h2>Welcome!</h2> : <h2>Please Sign In</h2>}

    {/* Logical AND */}
    {hasMessages && <p>You have new messages.</p>}
  </div>
);
```

---



