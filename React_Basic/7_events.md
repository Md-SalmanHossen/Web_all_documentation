## 📘 **React Event Handling: Step-by-Step Learning Guide**

### ✅ STEP 1: **What is Event Handling?**

* **কি জিনিস?** — User action (click, typing, submit) এর response এ ফাংশন চালানো।
* **JS vs React?** — JSX ব্যবহারের জন্য syntax একটু ভিন্ন।

---

### ✅ STEP 2: **Basic Event Handling**

* 👉 শুধুমাত্র `onClick`, `onChange` ইত্যাদিতে ফাংশন দেয়া শেখো।

📌 উদাহরণ:

```jsx
function App() {
  function handleClick() {
    alert("Hello!");
  }
  return <button onClick={handleClick}>Click</button>;
}
```

🧠 শিখো:

* `handleClick()` নয়, `handleClick` দিতে হয়।
* JSX-এ camelCase ইভেন্ট নাম (`onClick`, `onChange`)

---

### ✅ STEP 3: **Passing Arguments in Event**

📌 উদাহরণ:

```jsx
<button onClick={() => greet("সালমান")}>Greet</button>
```

🧠 শিখো:

* Arrow function দিয়ে কিভাবে আর্গুমেন্ট পাঠাতে হয়।
* Why not `greet("সালমান")` directly? (It'll run immediately)

---

### ✅ STEP 4: **Common DOM Events Table (onClick, onChange, onSubmit...)**

📚 মুখস্থ করো অথবা চিটশিট রাখো:

* `onClick` — Button
* `onChange` — Input
* `onSubmit` — Form
* `onKeyDown`, `onFocus`, `onBlur` — Input interactions

---

### ✅ STEP 5: **Event Object বুঝো**

📌 উদাহরণ:

```jsx
function handleClick(e) {
  console.log(e.target.value);
}
```

🧠 শিখো:

* `e` মানে `SyntheticEvent`
* `e.preventDefault()`, `e.stopPropagation()` শেখো

---

### ✅ STEP 6: **Form Handling (Controlled)**

📌 Focus: `useState`, `onChange`, `onSubmit`

```jsx
const [name, setName] = useState("");
<input value={name} onChange={(e) => setName(e.target.value)} />
<form onSubmit={handleSubmit}>...</form>
```

🧠 Step by Step:

* 1. State declare করো
* 2. Input value bind করো
* 3. Change handle করো
* 4. Submit এ preventDefault + logic চালাও

---

### ✅ STEP 7: **Props দিয়ে Event পাঠানো (Parent → Child)**

📌 উদাহরণ:

```jsx
function Child({ onClick }) {
  return <button onClick={onClick}>Click</button>;
}
```

🧠 শিখো:

* Props দিয়ে function pass করো
* Child → Event trigger → Parent function run

---

### ✅ STEP 8: **Event Phases (Capture → Target → Bubble)**

📌 শিখো:

* `onClickCapture`, `onClick`
* `stopPropagation()` দিয়ে bubbling বন্ধ
* Target phase মানে element নিজে, bubble মানে parent পর্যন্ত যাওয়া

---

### ✅ STEP 9: **Advanced Handling Techniques**

* Debounce Search Input:

  ```jsx
  useEffect(() => {
    const timeout = setTimeout(() => { ... }, 500);
    return () => clearTimeout(timeout);
  }, [input]);
  ```
* Prevent bubbling
* `useRef` দিয়ে Uncontrolled form handle

---

### ✅ STEP 10: **Best Practices Recap**

* Always use controlled input unless needed
* Use arrow functions for passing arguments
* Keep handlers outside JSX
* Use `e.preventDefault()` in form
* Avoid anonymous function in `onClick` for large apps

---

## 🔚 Bonus (পরের ধাপে পড়তে পারো):

* ✅ Custom Hooks দিয়ে event handling
* ✅ Keyboard Accessibility (keyup, keydown)
* ✅ Global Event (window scroll, resize) → `useEffect`

---

## 📌 Quick Practice Ideas:

| লেভেল    | প্রজেক্ট আইডিয়া                         |
| -------- | --------------------------------------- |
| Beginner | Click Counter, Input Mirror             |
| Mid      | Search with debounce                    |
| Advanced | Custom dropdown, File Upload with `ref` |

---
আমরা দুইটা জিনিস বুঝতে চাই:

---

## 🎯 বিষয় ১: **Event Handler-এ Props পাঠানো**

## 🎯 বিষয় ২: **Props দিয়ে Event Handler পাঠানো (Parent → Child)**

---

## 🟢 ১. Event Handler-এ Props পাঠানো (🔄 Props → Event handler)

---

### ✅ **🔍 কী?**

একটা কম্পোনেন্টের মধ্যে যখন আমরা ফাংশনের ভিতরে `props` ব্যবহার করি (যেমন: `props.name`, `props.onClick`), তখন সেটা বলা হয় — event handler-এ props পাঠানো।

---

### 📘 উদাহরণ ১: সিম্পল ক্লিক হ্যান্ডলার যেখানে `props.name` ব্যবহার হচ্ছে

```jsx
function GreetButton(props) {
  function handleClick() {
    alert(`হ্যালো, ${props.name}`);
  }

  return <button onClick={handleClick}>Say Hello</button>;
}

function App() {
  return <GreetButton name="সালমান" />;
}
```

#### 🔍 ব্যাখ্যা:

* `App` কম্পোনেন্ট `GreetButton`-এ `name="সালমান"` প্রপ্স পাঠিয়েছে
* `handleClick` ফাংশন `props.name` ব্যবহার করছে
* কাজেই এখানে **event handler এর ভিতরে props ব্যবহার হয়েছে**

---

### 📘 উদাহরণ ২: আর্গুমেন্টসহ props পাঠানো (advanced pattern)

```jsx
function GreetButton({ name }) {
  const handleClick = () => {
    alert(`Hello, ${name}`);
  };

  return <button onClick={handleClick}>Click me</button>;
}
```

➡️ এখানে আমরা props কে destructure করে নিয়েছি `({ name })`, এবং `handleClick`-এ ব্যবহার করেছি।

---

## 🟡 ২. Props দিয়ে Event Handler পাঠানো (Parent → Child)

---

### ✅ **🔍 কী?**

Parent কম্পোনেন্ট থেকে কোন ফাংশন (event handler) Child কম্পোনেন্টে props আকারে পাঠানো হয়।

### ⏰ **কখন দরকার হয়?**

* যখন চাইল্ড এলিমেন্টে ক্লিক করলে প্যারেন্টে কোনো অ্যাকশন চালাতে চাই
* বা চাইল্ড কিছু পাঠালে প্যারেন্ট সেটা হ্যান্ডল করবে

---

### 📘 উদাহরণ: Parent → Child event handler

```jsx
function Child({ onSayHello }) {
  return <button onClick={onSayHello}>Hello from Child</button>;
}

function Parent() {
  function handleHello() {
    alert("Parent বলছে: হ্যালো!");
  }

  return <Child onSayHello={handleHello} />;
}
```

#### 🔍 ব্যাখ্যা:

* Parent-এ `handleHello` নামে একটি ইভেন্ট হ্যান্ডলার আছে
* এটি `Child`-এ `onSayHello` নামে প্রপ্স আকারে পাঠানো হয়েছে
* `Child`-এ বাটন ক্লিক করলে সেই প্রপ্স-ফাংশন চালু হয়
* **এটা হলো: Props দিয়ে Event Handler পাঠানো**

---

### ✅ বাস্তব উদাহরণ: Form Input → প্যারেন্ট হ্যান্ডল

```jsx
function InputField({ onChangeInput }) {
  return <input type="text" onChange={(e) => onChangeInput(e.target.value)} />;
}

function App() {
  const [text, setText] = useState("");

  function updateText(value) {
    setText(value);
  }

  return (
    <div>
      <InputField onChangeInput={updateText} />
      <p>আপনি লিখেছেন: {text}</p>
    </div>
  );
}
```

#### 🔍 এখানে কী হচ্ছে?

* `App`-এ state আছে
* `updateText()` নামের হ্যান্ডলার ফাংশন `InputField`-এ প্রপ্স আকারে যাচ্ছে
* `InputField`-এ টাইপ করলে সেটা প্যারেন্ট state আপডেট করে
* **এটাই best practice: Child → Parent communication via props with event handler**

---

## 🔄 তুলনামূলক চিত্র:

| বিষয়                         | কোথা থেকে কোথায় যাচ্ছে           | লক্ষ্য                    |
| ---------------------------- | -------------------------------- | ------------------------- |
| Event handler-এ props পাঠানো | `props` কে ফাংশনের ভিতরে ব্যবহার | Dynamic message, behavior |
| Props দিয়ে event পাঠানো      | Parent → Child                   | Control child interaction |

---

## 💡 Extra: আর্গুমেন্টসহ props-এর মাধ্যমে ফাংশন পাঠানো

```jsx
function Child({ onClick }) {
  return <button onClick={() => onClick("from child")}>Click</button>;
}

function Parent() {
  const handleChildClick = (msg) => {
    alert(`Message ${msg}`);
  };

  return <Child onClick={handleChildClick} />;
}
```

✅ এখানে:

* `Child`-এ ফাংশন কল করে আর্গুমেন্ট পাঠানো হচ্ছে `onClick("from child")`
* `Parent`-এ সেই ফাংশন `msg` রিসিভ করে ব্যবহার করছে

---

## 📚 প্র্যাকটিস আইডিয়া:

| প্রজেক্ট নাম               | শিখতে পারবে                         |
| -------------------------- | ----------------------------------- |
| Counter Button             | Props → Event handler communication |
| Input Mirror Text          | Child → Parent value update         |
| Custom Alert Modal         | Child → Parent action               |
| Notification Toggle Button | Parent manages state from child     |

---

## ✅ উপসংহার:

> 🔹 **Event handler এ props পাঠানো** মানে হলো — ফাংশনের ভিতরে প্রপ্স ইউজ করা।
> 🔹 **Props দিয়ে event পাঠানো** মানে হলো — parent থেকে ফাংশন পাঠিয়ে child থেকে ট্রিগার করা।

---
#### একটা ফর্মে ইভেন্ট হ্যান্ডলিং React-এ বা JavaScript-এ শেখাটা অনেক জরুরি — কারণ প্রায় সব রিয়েল লাইফ অ্যাপে ইনপুট নেওয়া লাগে।


---

## 📌 কাঠামো:

1. **What is Form Event Handling?**
2. **When & Why we use it**
3. **Beginner Level Concepts**
4. **Intermediate Level Concepts**
5. **Advanced Level Concepts**
6. **Pseudocode Structure (from scratch)**
7. **Tips & Best Practices**

---

## 1️⃣ **🧠 What is Form Event Handling?**

Form event handling মানে হলো, ইউজার যখন কোনো ফর্ম ফিল্ডে টাইপ করে, সাবমিট করে, বা কোনো ইনপুটে ক্লিক করে — তখন সেসব event আমরা ধরে হ্যান্ডল করি।

🎯 উদাহরণঃ

* `onChange`: ইউজার input টাইপ করলে
* `onSubmit`: ইউজার form সাবমিট করলে
* `onFocus`, `onBlur`, `onClick`: ফিল্ডে ফোকাস বা ক্লিক করলে

---

## 2️⃣ ✅ **When & Why use Form Events**

* **Data collect করার জন্য** (input values)
* **Validation করার জন্য**
* **Database বা API তে পাঠানোর জন্য**
* **UI dynamically আপডেট করার জন্য**

---

## 3️⃣ 🟢 **Beginner Level Form Handling**

### 🎯 Basic Input Handling

#### 📘 Example:

```jsx
function BasicForm() {
  const [name, setName] = useState("");

  const handleChange = (event) => {
    setName(event.target.value);
  };

  const handleSubmit = (event) => {
    event.preventDefault(); // prevent page reload
    alert(`Submitted Name: ${name}`);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input type="text" onChange={handleChange} value={name} />
      <button type="submit">Submit</button>
    </form>
  );
}
```

### 🧠 কী শিখলাম:

* `useState` দিয়ে ইনপুট ট্র্যাক করা
* `onChange` দিয়ে ইনপুট আপডেট
* `onSubmit` এ সাবমিশন রোধ করে কাস্টম কাজ করা

---

## 4️⃣ 🟡 **Intermediate Form Handling Concepts**

### 📌 Topics:

* Multiple inputs
* Controlled vs Uncontrolled Components
* Basic validation

---

### 🧩 Example: Multiple fields

```jsx
function MultiInputForm() {
  const [form, setForm] = useState({ name: "", email: "" });

  const handleChange = (e) => {
    setForm({ ...form, [e.target.name]: e.target.value });
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    console.log("Form submitted:", form);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input name="name" onChange={handleChange} value={form.name} />
      <input name="email" onChange={handleChange} value={form.email} />
      <button type="submit">Submit</button>
    </form>
  );
}
```

### 🧠 এখানে শিখছিঃ

* Object structure দিয়ে একাধিক ইনপুট হ্যান্ডল
* `name` attribute ব্যবহার করে Dynamic update
* Cleaner state management

---

## 5️⃣ 🔴 **Advanced Form Handling Concepts**

### 📌 Topics:

* Validation (manual or library like Yup)
* File Upload
* Dynamic forms (add/remove fields)
* Integration with backend
* Error handling

---

### 🧩 Example: Form with validation + error

```jsx
function ValidatedForm() {
  const [email, setEmail] = useState("");
  const [error, setError] = useState("");

  const handleSubmit = (e) => {
    e.preventDefault();

    if (!email.includes("@")) {
      setError("Invalid email format");
      return;
    }

    setError("");
    console.log("Email submitted:", email);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input
        type="text"
        value={email}
        onChange={(e) => setEmail(e.target.value)}
      />
      {error && <p style={{ color: "red" }}>{error}</p>}
      <button type="submit">Submit</button>
    </form>
  );
}
```

✅ এখানে ইউজার ভুল ইনপুট দিলে Error দেখায়।
এটাই basic validation.

---

## 6️⃣ 📄 Pseudocode for Form Handling (Generic)

```
Initialize State for form fields
Define handleChange function
    - Take event as input
    - Update corresponding field value in state

Define handleSubmit function
    - Prevent default reload
    - Validate input
    - Show error or process form (API call / alert / console)

Create form with:
    - Input fields (with value and onChange)
    - Submit button with onSubmit
    - Conditional error rendering
```

---

## 🧠 Best Practices & Tips

✅ Use `name` attribute for multiple inputs
✅ Always prevent default form submission
✅ Validate before submitting
✅ Keep inputs "controlled" (bind with state)
✅ Break large forms into components
✅ Use libraries for complex forms: `Formik`, `React Hook Form`

---

## ✅ Bonus: Common Events You Should Know

| Event       | Use case              |
| ----------- | --------------------- |
| `onChange`  | Input টাইপ করলে       |
| `onSubmit`  | ফর্ম সাবমিট           |
| `onFocus`   | ফোকাসে গেলে           |
| `onBlur`    | ফোকাস হারালে          |
| `onClick`   | ক্লিক করলে            |
| `onKeyDown` | কীবোর্ড key প্রেস হলে |

---

## 🔚 শেষ কথা:

> Form Event Handling মানে শুধু ইনপুট নেওয়া না — বরং ইউজার ইন্টার‍্যাকশন বোঝা, ভ্যালিড করা, সাবমিট হ্যান্ডল করা এবং সেই ডেটা দিয়ে কাজ করা।

---
### Controlled vs Uncontrolled Input — এটা React-এ **form handling** শেখার অন্যতম গুরুত্বপূর্ণ টপিক।


---

## ✅ **1. What is Controlled vs Uncontrolled Input?**

| বিষয়             | Controlled Input                     | Uncontrolled Input                      |
| ---------------- | ------------------------------------ | --------------------------------------- |
| ডেটা কোথায় থাকে? | React state-এ                        | DOM এর ভিতরে (default browser behavior) |
| কে কন্ট্রোল করে? | React component (through `useState`) | Browser নিজেই                           |
| Access কীভাবে?   | `value` + `onChange`                 | `useRef` দিয়ে DOM থেকে                  |
| React friendly?  | হ্যাঁ (Recommended)                  | না (বিশেষ ক্ষেত্রে use করা যায়)         |

---

## 🎯 উদাহরণ দিয়ে বুঝি

---

### ✅ **Controlled Input Example**

```jsx
import { useState } from "react";

function ControlledInput() {
  const [name, setName] = useState(""); // React state

  const handleChange = (e) => {
    setName(e.target.value); // update state
  };

  return (
    <div>
      <input type="text" value={name} onChange={handleChange} />
      <p>Hi, {name}</p>
    </div>
  );
}
```

### 🔍 কী হলো এখানে?

* `value` React state দিয়ে কন্ট্রোল করা
* ইউজার input দিলেই `onChange` দিয়ে state আপডেট হয়
* React সবকিছু জানে — তাই predictable & manageable

---

### ❌ **Uncontrolled Input Example**

```jsx
import { useRef } from "react";

function UncontrolledInput() {
  const nameRef = useRef();

  const handleSubmit = () => {
    alert(`Your name is ${nameRef.current.value}`);
  };

  return (
    <div>
      <input type="text" ref={nameRef} />
      <button onClick={handleSubmit}>Show Name</button>
    </div>
  );
}
```

### 🔍 কী হলো এখানে?

* React জানে না ইনপুটের মধ্যে কী লিখছে ইউজার
* শুধু `ref` দিয়ে DOM access করে value নেয়া হচ্ছে
* এটাকে বলে uncontrolled — React control করছে না

---

## 🧠 Controlled Input: কখন ব্যবহার করবো?

✅ যখন আপনি চান:

* Form validation
* Dynamic input handling
* Input value দেখানো বা বদলানো
* Single source of truth (React state)

**🎯 Recommended for most use-cases in React**

---

## ⚠️ Uncontrolled Input: কখন ব্যবহার করবো?

✅ যখন:

* Quick performance দরকার (many fields but low interaction)
* 3rd-party library ব্যবহারে (like file uploads)
* খুব ছোট/simple forms
* DOM manipulation দরকার

---

## 🔍 তুলনামূলক চার্ট

| Feature            | Controlled         | Uncontrolled      |
| ------------------ | ------------------ | ----------------- |
| Performance        | Slow (large forms) | Faster            |
| Validation         | Easy               | Hard              |
| State access       | `useState`         | `useRef`          |
| React DevTools     | Value দেখা যায়     | দেখা যায় না       |
| File input support | Complicated        | Easier with `ref` |

---

## ✅ Suggestion (Beginner & Advanced উভয়ের জন্য):

* **React Developer হিসেবে ৯৫% সময় Controlled Input use করুন।**
* Uncontrolled use করুন শুধু special cases এ বা optimization দরকার হলে।

---

## 🔚 শেষ কথা:

> Controlled input হলো React-এর "নিজের ভাষায় কথা বলা", যেখানে state & UI পুরোপুরি synced থাকে।
> Uncontrolled input হলো traditional HTML-style handling, যেখানে React জানে না কী হচ্ছে।

---
নিচে React সহ ব্রাউজারের ইভেন্ট ফেজের **Capture → Target → Bubble** এই ৩টি ধাপ খুব সহজ ও বিস্তারিতভাবে ব্যাখ্যা :

---

## 🧠 ইভেন্টের ৩টি ধাপ: **Capture → Target → Bubble**

### 🔁 এই তিনটি ধাপ ব্রাউজারে যেকোনো DOM ইভেন্টের প্রাকৃতিক প্রবাহ বা ফ্লো বোঝায়।

---

### 🔰 ১. **Capture Phase (বা Capturing Phase)**

> **কী?**
> ইভেন্ট টপ-লেভেল এলিমেন্ট (window বা document) থেকে নিচের দিকে চাইল্ড এলিমেন্টে আসে, কিন্তু এখনও মূল টার্গেটে পৌঁছায়নি।

> **কখন হয়?**
> যখন আমরা ইভেন্ট হ্যান্ডলার ব্যবহার করি `{ capture: true }` দিয়ে, তখন এটা capture phase-এ কাজ করে।

> **React-এ কীভাবে কাজ করে?**
> React এ DOM-level capturing events সাধারণত `onClickCapture`, `onChangeCapture` এই রকমভাবে শুরু হয়।

> **উদাহরণ:**

```jsx
<div onClickCapture={() => console.log("Capture from Parent")}>
  <button onClick={() => console.log("Clicked")}>Click</button>
</div>
```

🟢 এখানে Parent-এর `onClickCapture` আগে ট্রিগার হবে, তারপর Button-এর `onClick`।

---

### 🎯 ২. **Target Phase**

> **কী?**
> এই ফেজে ইভেন্ট আসল যে এলিমেন্টে ঘটেছে (যেখানে ইউজার ক্লিক বা টাইপ করেছে), সেখানেই ট্রিগার হয়।

> **বুঝার টিপস:**
> এটা খুব ছোট ফেজ, যেখানে ইভেন্ট **target এলিমেন্ট**-এ পৌঁছে এবং সেখানেই প্রথম `onClick` বা `onChange` হয়।

> **উদাহরণ:**

```jsx
<button onClick={() => console.log("Button clicked")}>Click</button>
```

👉 এখানে শুধু এই বাটন ক্লিক করা হয়েছে, তাই এটি Target Phase এ ট্রিগার হবে।

---

### 🔄 ৩. **Bubble Phase (বা Bubbling Phase)**

> **কী?**
> Target এলিমেন্টে ইভেন্ট হ্যান্ডলার রান হওয়ার পর, ইভেন্ট উপরের দিকে প্যারেন্ট এলিমেন্ট গুলোতে ফিরে যেতে থাকে (bubble করে)।

> **ব্রাউজারে Default Behavior:**
> Bubble Phase ডিফল্ট। React-এও `onClick` বা `onChange` ইত্যাদি ইভেন্ট এই ফেজেই কাজ করে।

> **উদাহরণ:**

```jsx
<div onClick={() => console.log("Parent Clicked")}>
  <button onClick={() => console.log("Button Clicked")}>Click</button>
</div>
```

🟢 আউটপুট:

```
Button Clicked
Parent Clicked
```

👉 প্রথমে Target (Button), তারপর Bubble করে Parent-এ।

---

## 📌 তুলনামূলক চার্ট

| ধাপ         | কোন দিক থেকে কোন দিকে | কীভাবে React-এ পাওয়া যায়     |
| ----------- | --------------------- | ---------------------------- |
| **Capture** | parent ➡️ child       | `onClickCapture`             |
| **Target**  | যেখানে ইভেন্ট ঘটেছে   | `onClick`, `onChange`        |
| **Bubble**  | child ➡️ parent       | `onClick` (default bubbling) |

---

## 🚫 ইভেন্ট বাবল বন্ধ করতে চাইলে:

```jsx
function handleClick(e) {
  e.stopPropagation(); // ইভেন্ট আর প্যারেন্টে যাবে না
}
```

---

## 🎯 রিয়েল লাইফ উদাহরণ:

ধরো, তুমি একটা টেবিলে বসে আছো (Button), টেবিল একটা রুমে আছে (Div), আর রুম একটা বাড়িতে (Body)।

* **Capture Phase**: বাড়ি ➡️ রুম ➡️ টেবিল
* **Target Phase**: টেবিলেই একশনে ঘটনা ঘটে
* **Bubble Phase**: টেবিল ➡️ রুম ➡️ বাড়ি পর্যন্ত আবার ফিরে যায়

---

## 💡 প্র্যাকটিস করার জন্য Mini Projects:

| প্রজেক্ট নাম             | শিখতে পারবে                       |
| ------------------------ | --------------------------------- |
| ইভেন্ট ট্র্যাকার         | Capture vs Bubble log             |
| মেনু হোভার + ক্লিক       | Event Bubbling vs stopPropagation |
| Nested Button click      | Target Phase demo                 |
| Custom modal click-close | Bubble control                    |

---

## 🔚 উপসংহার

> **Capture → Target → Bubble** হলো DOM ইভেন্টের স্বাভাবিক পথ।
> React-এ `onClick` ও `onClickCapture` ব্যবহার করে তুমি পুরো ইভেন্ট ফ্লো কন্ট্রোল করতে পারো।
> Advanced UI বা ফর্মে এটি জানা অত্যন্ত গুরুত্বপূর্ণ।

---

## 🧠 React Event Handling – Interview Questions & Answers

---

### ✅ Beginner Level

---

### 1️⃣ **React-এ Event Handling কী?**

**উত্তর:**
React-এ Event Handling হলো ব্যবহারকারীর Action (যেমন ক্লিক, টাইপিং, সাবমিট) এর response-এ কোনো function execute করা। এটি JSX syntax ব্যবহার করে এবং SyntheticEvent অবজেক্ট রিটার্ন করে।

---

### 2️⃣ **React-এ onClick event handle করার সঠিক পদ্ধতি কী?**

**উত্তর:**

```jsx
<button onClick={handleClick}>Click me</button>
```

ফাংশন reference (`handleClick`) দিতে হয়, `handleClick()` নয় — নয়তো তা Component render হওয়ার সময়েই execute হয়ে যাবে।

---

### 3️⃣ **SyntheticEvent কী?**

**উত্তর:**
React এর ইভেন্ট সিস্টেম একটি wrapper ব্যবহার করে যাকে বলা হয় `SyntheticEvent`। এটি browser এর native event-এর ওপর একটি ক্রস-ব্রাউজার compatible abstraction।

---

### 4️⃣ **onChange এবং onInput-এর মধ্যে পার্থক্য কী?**

**উত্তর:**

* `onChange` → Input field-এর মান পরিবর্তনের পর trigger হয় (blur বা submit-এ)
* `onInput` → প্রতিটি টাইপ করার সময় trigger হয় (realtime)
  React-এ `onChange` behaves like native `onInput`.

---

### ✅ Intermediate Level

---

### 5️⃣ **Form সাবমিট হ্যান্ডল করার পদ্ধতি কী?**

**উত্তর:**

```jsx
function handleSubmit(e) {
  e.preventDefault();
  // logic
}
```

`e.preventDefault()` দিয়ে browser reload হওয়া বন্ধ করতে হয়।

---

### 6️⃣ **কীভাবে argument সহ event handler কল করো?**

**উত্তর:**

```jsx
<button onClick={() => handleClick('সালমান')}>Click</button>
```

Arrow function ব্যবহার করে আর্গুমেন্ট পাঠানো হয়।

---

### 7️⃣ **Parent থেকে Child-এ event function কিভাবে পাঠাতে হয়?**

**উত্তর:**

```jsx
<Child onButtonClick={handleClick} />
```

Child component props হিসেবে function নেয় এবং প্রয়োজনে কল করে।

---

### 8️⃣ **Event bubbling এবং stopPropagation() ব্যাখ্যা করো।**

**উত্তর:**
Event bubbling হলো ইভেন্ট একাধিক লেভেলে propagate হওয়া (child → parent)।
`e.stopPropagation()` কল করলে ইভেন্ট উপরের DOM element এ পৌঁছায় না।

---

### ✅ Advanced Level

---

### 9️⃣ **Controlled vs Uncontrolled Input এর পার্থক্য কী?**

| Controlled Input                | Uncontrolled Input                  |
| ------------------------------- | ----------------------------------- |
| React state দিয়ে নিয়ন্ত্রিত     | React state ছাড়া DOM থেকে নিয়ন্ত্রণ |
| `value` ও `onChange` ব্যবহার হয় | `defaultValue` ও `ref` ব্যবহার হয়   |

---

### 🔟 **Debounce কাকে বলে এবং কেন দরকার?**

**উত্তর:**
Debounce মানে user প্রতিবার টাইপ করার সাথে সাথে API call না করে delay দিয়ে wait করা। Performance উন্নত করার জন্য ব্যবহৃত হয়।

```jsx
useEffect(() => {
  const timer = setTimeout(() => search(query), 500);
  return () => clearTimeout(timer);
}, [query]);
```

---

### 1️⃣1️⃣ **Event capturing এবং bubbling এর মধ্যে পার্থক্য কী?**

| Capturing Phase               | Bubbling Phase           |
| ----------------------------- | ------------------------ |
| Event উপরের দিক থেকে নিচে আসে | Event নিচ থেকে উপরে যায় |
| `onClickCapture` ব্যবহার হয়   | `onClick` ব্যবহার হয়     |

---

### 1️⃣2️⃣ **Custom event handler logic reusable করতে কী ব্যবহার করো?**

**উত্তর:**
Custom hook ব্যবহার করা হয়। উদাহরণ:

```jsx
function useInput() {
  const [value, setValue] = useState('');
  const handleChange = (e) => setValue(e.target.value);
  return { value, onChange: handleChange };
}
```

---

### ⚠️ Bonus: Tricky Interview Questions

* 📌 Why should we avoid inline arrow functions in large components?

  > প্রতিবার render-এ নতুন ফাংশন তৈরি হয়, performance degrade হতে পারে।

* 📌 What is the difference between `e.target` and `e.currentTarget`?

  > `e.target`: যেই element এ ইভেন্ট ঘটেছে
  > `e.currentTarget`: যেই element এ listener অ্যাটাচ করা হয়েছে

---

## 💼 Practice Prompt(if you need):

> আপনার কাছে একটি সার্চ বক্স এবং একটি সাবমিট বাটন আছে। যেকোনো নাম টাইপ করলে ডিবাউন্স করে রেজাল্ট দেখাবে এবং সাবমিট করলে `alert` দিবে। — **এই জিনিসটা বানাও।**

---








