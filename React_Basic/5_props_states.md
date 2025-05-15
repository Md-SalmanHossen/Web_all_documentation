## 🟡 PROPS (Properties): Data passed into a component

### 🔹 What it is:

Props হলো function-এর parameter-এর মতো। তুমি যখন কোনো component call করো, তখন তুমি props দিয়ে values পাঠাতে পারো।

### 🔹 কিভাবে কাজ করে:

1. Props are passed from parent to child component
2. Props are immutable (change করা যায় না inside the child)
3. You access props like: props.name বা directly via destructuring: ({ name })

📦 উদাহরণ:

```jsx
function StudentProfile({ name, age }) {
  return (
    <div>
      <h2>{name}</h2>
      <p>Age: {age}</p>
    </div>
  );
}

// Using the component:
<StudentProfile name="Rafi" age={22} />
```

👉 এখানে name ও age props হিসেবে পাঠানো হয়েছে। Child component শুধু এগুলো receive করে — modify করতে পারে না।

### 🔸 Props এর বৈশিষ্ট্য:

| Feature         | Description                           |
| --------------- | ------------------------------------- |
| Direction       | Parent → Child                        |
| Change allowed? | না (Read-only)                        |
| Usage           | Static বা dynamic data pass করা       |
| Syntax          | JSX tag এর মধ্যে attribute আকারে      |
| Example         | `<MyComponent title="Hello World" />` |

---

## 🔁 Props vs State: Deep Difference Table

| Feature           | Props                         | State                           |
| ----------------- | ----------------------------- | ------------------------------- |
| Mutability        | Immutable (read-only)         | Mutable (can be updated)        |
| Scope             | Passed from parent            | Owned by the component          |
| Use Case          | Data passing, configuration   | Dynamic UI, user interaction    |
| How to define     | JSX attributes                | useState/useReducer             |
| Change by?        | Parent only                   | Component itself (via setState) |
| Causes re-render? | No (unless parent re-renders) | Yes                             |

---

## 🧠 When to use Props vs State?

✅ Use props when:

* তুমি child component কে data পাঠাতে চাও
* Component static/informational
* Component reusability দরকার

✅ Use state when:

* Data dynamically change হবে
* User interaction আছে (click, input, etc.)
* UI কে dynamically update করতে হবে

---

## 🔄  Combining Props and State

তুমি props ও state একসাথে ব্যবহার করতে পারো:

```jsx
function Greeting({ name }) {
  const [isMorning, setIsMorning] = useState(true);

  return (
    <h1>
      Good {isMorning ? 'Morning' : 'Evening'}, {name}!
      <button onClick={() => setIsMorning(!isMorning)}>Switch</button>
    </h1>
  );
}
```

👉 এখানে name এসেছে props থেকে, আর isMorning এসেছে state থেকে।

---

📌 Bottom Line:

* props হচ্ছে external data → তুমি বাইরে থেকে পাঠাও
* state হচ্ছে internal data → তুমি ভিতরে থেকে manage করো
* props change হয় parent দ্বারা, state change হয় নিজেই
* props read-only, state mutable
* দুটোই important — static & dynamic UI তৈরির জন্য


React-এর **props** (properties) হল এক কম্পোনেন্ট থেকে আরেক কম্পোনেন্টে **ডেটা পাঠানোর উপায়**। এই ডেটা পাঠানো সবসময় **parent → child** (অভিভাবক → শিশু) দিকেই হয়, অর্থাৎ **unidirectional data flow** (একমুখী ডেটা প্রবাহ)।

---



**Props**:
➡️ **Parent component** তার **Child component**-কে ডেটা (value/function) পাঠায়
➡️ Child শুধুমাত্র সেই ডেটা receive করে এবং ব্যবহার করে
➡️ Props কখনো modify করা যায় না — এগুলো **read-only**

---

## 📦 উদাহরণ ১: বেসিক props পাঠানো

```jsx
// Parent Component
function App() {
  return <Welcome name="রহিম" />;
}

// Child Component
function Welcome(props) {
  return <h1>হ্যালো, {props.name}!</h1>;
}
```

🔍 এখানে `App` হচ্ছে parent, ও `Welcome` হচ্ছে child। `name="রহিম"` props আকারে পাঠানো হয়েছে।

---

## 🧩 Props কে যেভাবে ব্যাবহার করা হয়:

```jsx
function Child(props) {
  return <p>{props.message}</p>;
}
```

অথবা **destructuring** করে:

```jsx
function Child({ message }) {
  return <p>{message}</p>;
}
```

---

## 🔁 Advanced Concept: Nested Props, Functions, and Dynamic Use

### 📌 ১. Function পাঠানো (callback props):

```jsx
function Parent() {
  const handleClick = () => {
    alert('বাটন ক্লিক হয়েছে!');
  };

  return <Child onClick={handleClick} />;
}

function Child({ onClick }) {
  return <button onClick={onClick}>ক্লিক করো</button>;
}
```

🔍 এখানে function `handleClick` পাঠানো হয়েছে child এ, এবং child তা ব্যবহার করছে।

---

### 📌 ২. Complex object পাঠানো:

```jsx
function App() {
  const user = { name: "Karim", age: 25 };
  return <Profile info={user} />;
}

function Profile({ info }) {
  return <p>{info.name} - {info.age} বছর</p>;
}
```

---

### 📌 ৩. Children props (component এর ভিতরের content):

```jsx
function Card({ children }) {
  return <div className="card">{children}</div>;
}

function App() {
  return (
    <Card>
      <h2>এইটা একটা কার্ডের ভিতরের content</h2>
    </Card>
  );
}
```

🔍 `children` props automatic পাঠানো হয় component এর opening এবং closing tag এর মাঝে যা থাকে তা দিয়ে।

---

## 🧭 Summary (সারাংশ):

| বিষয়             | ব্যাখ্যা                                                           |
| ---------------- | ------------------------------------------------------------------ |
| Props কি?        | এক component থেকে আরেকটিতে data/function পাঠানোর উপায়             |
| Flow             | শুধু Parent → Child                                                |
| Modify করা যায়? | না, props শুধু পড়া যায় (read-only)                               |
| Use cases        | Text পাঠানো, Function পাঠানো, Object/Array পাঠানো, Child rendering |

---

ভালো প্রশ্ন! ✅
**Props vs Lifting State Up** – দুটোই React-এ component এর মধ্যে যোগাযোগের জন্য ব্যবহৃত হয়, কিন্তু এদের কাজ আলাদা।

---

## 🔁 Props: (Parent → Child)

➡️ **Data শুধু উপর থেকে নিচে যায়** (parent → child)
➡️ Props দিয়ে শুধুই data/function পাঠানো যায়
➡️ Example:

```jsx
function Parent() {
  return <Child message="Hello" />;
}

function Child({ message }) {
  return <p>{message}</p>;
}
```

---

## ⬆️ Lifting State Up: (Child → Parent)

➡️ যখন দুইটি sibling component বা nested child-এর **মধ্যে data share** করতে হয়
➡️ তখন **parent** এ state রাখি, এবং **child** গুলোকে সেই state বা update function props হিসেবে পাঠাই
➡️ এতে child → parent এ data “উঠে যায়” (lift)
➡️ Example:

```jsx
function Parent() {
  const [name, setName] = useState("");

  return (
    <>
      <InputComponent onNameChange={setName} />
      <DisplayComponent name={name} />
    </>
  );
}

function InputComponent({ onNameChange }) {
  return (
    <input
      onChange={(e) => onNameChange(e.target.value)}
      placeholder="নাম লিখুন"
    />
  );
}

function DisplayComponent({ name }) {
  return <h1>নাম: {name}</h1>;
}
```

🔍 এখানে `InputComponent` তার input value `setName` এর মাধ্যমে **Parent এ তোলে**, এবং `DisplayComponent` সেই state read করে।

---

## ✅ কবে কোনটা ব্যবহার করবো?

| তুমি চাইলে...               | ব্যবহার করো        |
| --------------------------- | ------------------ |
| শুধু ডেটা পাঠাতে            | `props`            |
| চাইল্ড থেকে ডেটা উপরে তুলতে | `lifting state up` |

---
নিচে React এর **props** নিয়ে ২০টি গুরুত্বপূর্ণ ইন্টারভিউ প্রশ্ন ও উত্তর **বাংলা**তে দেয়া হলো — সহজ থেকে জটিল পর্যায়ে।

---

## 🔰 Beginner Level (প্রাথমিক)

1. **Props কী?**
   📌 Props (properties) হল React এর মাধ্যমে parent component থেকে child component এ পাঠানো read-only মান বা data।

2. **Props কীভাবে পাঠানো হয়?**
   📌 JSX-এ attributes এর মতো লিখে পাঠানো হয়:

   ```jsx
   <User name="Rahim" />
   ```

3. **Props কীভাবে access করা হয়?**
   📌 Function component-এ parameter দিয়ে:

   ```jsx
   function User(props) {
     return <p>{props.name}</p>;
   }
   ```

4. **Props কি পরিবর্তনযোগ্য (mutable)?**
   ❌ না, props কখনো পরিবর্তন করা যায় না; এগুলো read-only।

5. **Child component থেকে props পরিবর্তন করা যায় কি?**
   ❌ না, শুধু parent থেকেই props পরিবর্তন করে পাঠানো যায়।

---

## 🧠 Intermediate Level (মধ্যম স্তর)

6. **Props আর state এর মধ্যে পার্থক্য কী?**
   📌 Props আসে parent থেকে এবং read-only, state থাকে component-এর ভিতরে এবং changeable।

7. **Functional component কি props নিতে পারে?**
   ✅ হ্যাঁ, সব component (class বা function) props নিতে পারে।

8. **যদি কোনো prop না পাঠানো হয় তাহলে কী হয়?**
   📌 ওই prop `undefined` হবে, যদি না default value সেট করা থাকে।

9. **Functional component-এ default props কীভাবে সেট করব?**

   ```jsx
   function User({ name = "Guest" }) {
     return <p>{name}</p>;
   }
   ```

10. **`props.children` কী?**
    📌 Component tag এর ভিতরের content কে React `children` props হিসেবে ধরে।

    ```jsx
    <Card>Hello World</Card>
    ```

---

## 🧪 Advanced Level (উন্নত)

11. **Props drilling কী?**
    📌 এক component থেকে অন্য component-এ props forward করতে করতে অনেক লেভেল পার হয়ে যাওয়াকে props drilling বলে।

12. **Props drilling এড়াতে কী ব্যবহার করা হয়?**
    📌 Context API, Redux বা Zustand ব্যবহার করে।

13. **Function কি props হিসেবে পাঠানো যায়?**
    ✅ হ্যাঁ, event handle বা callback হিসেবে পাঠানো যায়।

    ```jsx
    <Button onClick={handleClick} />
    ```

14. **Spread operator দিয়ে props পাঠানো মানে কী?**
    📌 একাধিক props একসাথে পাঠানো:

    ```jsx
    const user = { name: "Ali", age: 30 };
    <User {...user} />
    ```

15. **propTypes কী?**
    📌 Component এ পাঠানো props এর type validate করার জন্য `prop-types` প্যাকেজ ব্যবহার করা হয়।

---

## 🧩 Expert Level (দুর্দান্ত)

16. **propTypes ভুল হলে কী হয়?**
    📌 Console-এ warning দেখায় (development mode-এ), কিন্তু অ্যাপ চলে।

17. **Nested object বা complex shape prop কিভাবে validate করব?**

    ```jsx
    User.propTypes = {
      user: PropTypes.shape({
        name: PropTypes.string,
        age: PropTypes.number,
      }),
    };
    ```

18. **Props পরিবর্তিত হলে কি component re-render হয়?**
    ✅ হ্যাঁ, যদি props এর মান পরিবর্তিত হয়, component নতুন করে render হয়।

19. **Memoization কীভাবে props এর সাথে কাজ করে?**
    📌 `React.memo()` ব্যবহার করলে একই props থাকলে component re-render হয় না।

    ```jsx
    const MyComponent = React.memo(function MyComponent(props) {
      return <div>{props.value}</div>;
    });
    ```

20. **কখন `useCallback` ব্যবহার করব props এর ক্ষেত্রে?**
    📌 যখন কোনো function props হিসেবে memoized component এ পাঠানো হয় এবং চাই unnecessary re-render না হোক।

---


## 🧠 কেন `props` শুধুমাত্র **read-only**?

> 📌 কারণ React এ **data flow একমুখী (one-way)** — মানে parent component থেকে child component এ ডাটা যায়। তাই props কখনো পরিবর্তনযোগ্য (mutable) না।

---

### 🔍 সহজভাবে ধরো:

ধরো, **Parent component** তার **Child component** কে কিছু data পাঠাচ্ছে (যেমন নাম বা সংখ্যা)। এখন যদি child component সেই data (props) ইচ্ছামতো পরিবর্তন করতে পারে, তাহলে React-এর data control system **অরাজক হয়ে যাবে**।

তাই React বলে:

> ❗ "**Props শুধুমাত্র পড়া যাবে (read-only)**। যদি তুমি কিছু পরিবর্তন করতে চাও, তাহলে সেটি **Parent এর state পরিবর্তন করে** নতুন props হিসেবে পাঠাও।"

---

### 🎯 উদাহরণ দিয়ে বোঝানো:

```jsx
function Parent() {
  const [name, setName] = useState("রহিম");
  return <Child name={name} />;
}

function Child(props) {
  props.name = "করিম"; // ❌ এটা ভুল! props পরিবর্তন করা যাবে না
  return <p>{props.name}</p>;
}
```

উপরের কোডে `props.name` পরিবর্তন করতে চাইলেও React এটা **সমর্থন করে না**।

---

### ✅ তাহলে পরিবর্তন করব কীভাবে?

Parent component-এ state রেখে child কে function পাঠাও:

```jsx
function Parent() {
  const [count, setCount] = useState(0);

  return <Child count={count} onIncrement={() => setCount(count + 1)} />;
}

function Child({ count, onIncrement }) {
  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={onIncrement}>+1</button>
    </div>
  );
}
```

এভাবে child button ক্লিক করলে parent এর state পরিবর্তন হয়, আর নতুন props আকারে child এ আসে।

---

### 📊 সংক্ষেপে কারণগুলো:

| কারণ                     | ব্যাখ্যা                                 |
| ------------------------ | ---------------------------------------- |
| একমুখী ডাটা প্রবাহ       | Parent → Child — সহজ, পরিষ্কার data flow |
| Predictable behavior     | কে কোথা থেকে data পাচ্ছে, বোঝা সহজ       |
| Bug কম হয়                | যেহেতু কেউ props পরিবর্তন করতে পারে না   |
| Performance optimization | React সহজে বুঝে কবে re-render করতে হবে   |

---

### 🔐 মনে রাখো:

> 🔄 Props পরিবর্তন করতে চাইলে Parent-এর state পরিবর্তন করো।

---





