## React Component Thinking Master Guide 


## 🔷 Part 1: How to **Think in Components**

React-এর মূল মন্ত্র:

> **"Divide and Conquer the UI"**

মানে: তোমার UI-কে একসাথে ধরলে মাথা গুলিয়ে যাবে। তাই তাকে ভাগ করো ছোট ছোট **manageable components** এ।

---

## 🧩 Step-by-Step Breakdown

---

### 🔹 Step 1: Start from UI Layout

Figma file বা wireframe থেকে শুরু করো।

**চিন্তা করো:**

* কোন অংশটা repeatable?
* কোন অংশটা isolate করে চালানো যায়?
* কোথায় interaction থাকবে (click, type, scroll)?

📦 Example Layout:

```
Page
├── Navbar
├── ProductList
│   ├── ProductCard
│   ├── ProductCard
├── CartSidebar
└── Footer
```

---

### 🔹 Step 2: Break UI into Logical Boxes

> **"যেখানে visually বা functionally আলাদা — সেখানে আলাদা component হওয়া উচিত।"**

Example (Livestock App):

```
Dashboard
├── Header
├── Sidebar
├── MainContent
│   ├── LivestockList
│   │   ├── LivestockItem
│   ├── HealthStats
│   └── UpcomingTasks
└── Footer
```

---

### 🔹 Step 3: Reusable vs Specific Component চিন্তা করো

#### ✅ **Reusable Components**

Generic – যেকোনো জায়গায় use করা যায়
👉 Stateless / props-driven
👉 UI focus heavy

🧠 Examples:

* `Button`, `Modal`, `Card`, `InputField`, `Avatar`

```jsx
<Button label="Save" onClick={handleSave} />
<Button label="Delete" variant="danger" />
```

---

#### 🎯 **Specific Components**

Context-specific – এক particular feature বা page-এর জন্য
👉 Data-aware
👉 Logic-heavy

🧠 Examples:

* `LivestockProfile`, `HealthStats`, `UpcomingTasks`

```jsx
const LivestockProfile = ({ animalId }) => {
  const [animal, setAnimal] = useState(null);
  useEffect(() => {
    fetch(`/api/livestock/${animalId}`)
      .then(res => res.json())
      .then(data => setAnimal(data));
  }, [animalId]);

  return animal ? (
    <Card>
      <h2>{animal.name}</h2>
    </Card>
  ) : <Loader />;
};
```

---

### 🔹 Step 4: Component Types (💥 Deep Dive)

| Type                      | Description                           | Example                      |
| ------------------------- | ------------------------------------- | ---------------------------- |
| **Presentational (Dumb)** | শুধু UI দেখায়, logic নাই              | `Card`, `Badge`, `Loader`    |
| **Container (Smart)**     | State & data fetch করে                | `LivestockListContainer`     |
| **Higher-Order (HOC)**    | Component কে wrap করে feature যোগ করে | `withAuth`, `withLogger`     |
| **Layout**                | Page structure define করে             | `DashboardLayout`, `GridRow` |

🧠 Example Pair:

```jsx
// Dumb
const LivestockItem = ({ name }) => <div>{name}</div>;

// Smart
const LivestockList = () => {
  const [animals, setAnimals] = useState([]);
  useEffect(() => {
    fetch('/api/livestock')
      .then(res => res.json())
      .then(setAnimals);
  }, []);
  return animals.map(a => <LivestockItem {...a} />);
};
```

---

## 🎯 Real-Life Component Classification (Livestock App)

| Component   | Static/Dynamic | Role             | Type            |
| ----------- | -------------- | ---------------- | --------------- |
| Navbar      | Static         | Layout           | Static Layout   |
| Footer      | Static         | Layout           | Static Layout   |
| ProductList | Dynamic        | Data-driven list | Smart Container |
| ProductCard | Repeatable     | Visual unit      | Dumb UI         |
| CartSidebar | Interactive    | Cart logic       | Smart Component |

---

## 🔁 Reusable vs Specific Component – Full Table

| Feature     | **Reusable**              | **Specific**                     |
| ----------- | ------------------------- | -------------------------------- |
| Purpose     | General use               | Domain-focused                   |
| Usage Count | Multiple places           | One place                        |
| Data Logic  | Stateless / props only    | Own API/state                    |
| Flexibility | Customizable via props    | Fixed purpose                    |
| Examples    | `Button`, `Modal`, `Card` | `HealthStats`, `VetConsultModal` |

---

## 💎 Component Creation Thinking Strategy

### 1️⃣ Reusable বানাতে চাইলে:

✅ Props-driven রাখো
✅ Pure UI focus করো
✅ No side-effects or API

### 2️⃣ Specific বানাতে চাইলে:

✅ Stateful রাখো
✅ Data fetch করো
✅ Parent-child logic maintain করো

---

## 📌 Rule of Thumb – Shortcut Logic

| Question                                                 | If Yes →         |
| -------------------------------------------------------- | ---------------- |
| "Can I reuse this anywhere with just props?"             | ✅ Reusable       |
| "Is this tied to my app's domain or logic-heavy?"        | 🎯 Specific      |
| "Does it have its own API, state, or side effects?"      | 🎯 Specific      |
| "Is it part of layout (Navbar/Footer) but fixed/static?" | 🧱 Static Layout |

---

## ✅Tips :

* Start from **presentational**, then wrap with **container**
* Reuse small UI parts (Card, Button) to reduce duplication
* Always **name smartly** – e.g., `LivestockItem` vs `Card`
* Components ছোট রাখো (SRP – Single Responsibility Principle)

---

## 🔚 Final Summary

🟢 Reusable = **Tools** (flexible, props-driven, generic UI)
🔵 Specific = **Features** (data logic, app-specific, smart components)

React-এ Component চিন্তা করা মানে হচ্ছে:

> **"UI কে টুকরো করে চিন্তা করো – যেটা repeatable, সেটা generalize করো, আর যেটা app-specific, সেটা আলাদা করো।"**

---
**Control component** (বা **controlled component**) React এ এমন একটা component যেটার input element গুলোর মান (value) React state দ্বারা নিয়ন্ত্রিত হয়।

### 🧠 সংজ্ঞা:

> A **controlled component** is an input form element (like `<input>`, `<textarea>`, `<select>`) whose value is **controlled by React state**.

---

### 🎯 সাধারণ উদাহরণ:

```jsx
import { useState } from "react";

function ControlledForm() {
  const [name, setName] = useState(""); // state দিয়ে নিয়ন্ত্রণ করা হচ্ছে

  const handleChange = (e) => {
    setName(e.target.value); // input এর মান state এ সেট হচ্ছে
  };

  return (
    <div>
      <input type="text" value={name} onChange={handleChange} />
      <p>Your name: {name}</p>
    </div>
  );
}
```

এখানে `input` এর `value={name}` — মানে হচ্ছে input এর মানটা React এর `name` state থেকে আসছে। এই input কে আমরা বলি **controlled component**।

---

### 🆚 Controlled vs Uncontrolled Component

| Feature            | Controlled Component | Uncontrolled Component |
| ------------------ | -------------------- | ---------------------- |
| Value managed by   | React `state`        | DOM (internal)         |
| Uses `value` prop? | ✅ হ্যাঁ              | ❌ না                   |
| Access data via    | React                | `ref` দিয়ে DOM access  |
| Example            | `value={name}`       | `defaultValue="John"`  |

---

### ✅ কেন Controlled Component ব্যবহার করব?

1. Form এর উপরে পুরা নিয়ন্ত্রণ থাকে।
2. Input validate করা সহজ।
3. State synchronize রাখা যায় সহজে।
4. Complex interaction handle করা যায় (like enabling submit button when valid).

---

ভালো, তাহলে এবার একটি **Uncontrolled Component** এর উদাহরণ দেখাই — যাতে তুমি বুঝতে পারো controlled আর uncontrolled এর পার্থক্য কীভাবে কাজ করে।

---

### 🤖 Uncontrolled Component (React)

```jsx
import { useRef } from "react";

function UncontrolledForm() {
  const inputRef = useRef(null);

  const handleSubmit = (e) => {
    e.preventDefault();
    alert("Name is: " + inputRef.current.value); // DOM থেকে সরাসরি মান নিচ্ছে
  };

  return (
    <form onSubmit={handleSubmit}>
      <input type="text" ref={inputRef} defaultValue="John Doe" />
      <button type="submit">Submit</button>
    </form>
  );
}
```

এখানে `value` React state দ্বারা নিয়ন্ত্রিত না, বরং DOM এর `ref` দিয়ে সরাসরি অ্যাক্সেস করে মান নেওয়া হচ্ছে। একে বলে **Uncontrolled Component**।

---

### 🧠 Summary:

| Feature               | Controlled               | Uncontrolled         |
| --------------------- | ------------------------ | -------------------- |
| মান কোথা থেকে আসে?    | React `useState`         | DOM (`ref`)          |
| রিয়াল-টাইম ভ্যালিডেশন | সহজ                      | তুলনামূলক কঠিন       |
| Reset বা Clear করা    | state update করলেই সম্ভব | DOM এ সরাসরি করতে হয় |
| Complex Form Logic    | অনেক সহজ                 | কঠিন                 |

---
 নিচে React এর **component** সম্পর্কিত ২০টি interview প্রশ্ন এবং উত্তর দেওয়া হলো বাংলায়, বিভিন্ন লেভেল অনুযায়ী:

---

## 🔰 Beginner Level (প্রাথমিক)

1. **React Component কী?**
   📌 Component হচ্ছে React এর সবচেয়ে ছোট building block যা UI তৈরি করে। প্রতিটি Component একটি JavaScript ফাংশন বা ক্লাস যা HTML রিটার্ন করে।

2. **React Component ক’প্রকার?**
   📌 দুই প্রকার:

   * **Functional Component**
   * **Class Component**

3. **Functional Component কী? উদাহরণ দাও।**
   📌 একটি simple JavaScript function যা JSX return করে।

   ```jsx
   function Hello() {
     return <h1>Hello, World!</h1>;
   }
   ```

4. **Class Component কী? উদাহরণ দাও।**
   📌 `React.Component` থেকে extend করে তৈরি করা component।

   ```jsx
   class Hello extends React.Component {
     render() {
       return <h1>Hello, World!</h1>;
     }
   }
   ```

5. **Functional vs Class Component এর পার্থক্য কী?**
   📌 Functional Component সহজ, কিন্তু ক্লাস component এ state, lifecycle method আগে পর্যন্ত ছিল (React 16.8 এর আগে)। এখন hook ব্যবহারে দুইটাতেই একই কাজ করা যায়।

---

## 🧠 Intermediate Level (মধ্যম স্তর)

6. **JSX কী?**
   📌 JSX হচ্ছে JavaScript এর ভিতরে HTML এর মতো syntax যা React এ UI define করতে ব্যবহৃত হয়।

7. **Component reusability কীভাবে কাজ করে?**
   📌 Component বানিয়ে বারবার বিভিন্ন জায়গায় ব্যবহার করা যায়, আলাদা props দিয়ে কাস্টমাইজ করা যায়।

8. **Component render কবে হয়?**
   📌 যখন component প্রথমবার DOM এ যায় বা তার props/state পরিবর্তন হয়।

9. **Stateless এবং Stateful Component এর পার্থক্য কী?**
   📌 Stateless component শুধু props নেয়, state handle করে না। Stateful component নিজস্ব state ম্যানেজ করে।

10. **Controlled Component কী?**
    📌 এমন input element যার মান React state দ্বারা নিয়ন্ত্রিত হয়।

---

## 🧪 Advanced Level (উন্নত)

11. **What is a Higher-Order Component (HOC)?**
    📌 একটি function যা component নেয় এবং সেটিকে নতুন behavior সহ return করে।
    Example: `withAuth(Component)`

12. **Pure Component কী?**
    📌 এমন component যেটা shallow comparison এর মাধ্যমে বুঝতে পারে যে props/state পরিবর্তন হয়েছে কিনা, এবং সেই অনুযায়ী render করে।

13. **Lazy loading component কীভাবে করে?**
    📌 `React.lazy()` এবং `Suspense` দিয়ে করা হয়।

    ```jsx
    const MyComponent = React.lazy(() => import('./MyComponent'));
    ```

14. **Dynamic component rendering কীভাবে হয়?**
    📌 Props বা state অনুযায়ী component conditionally return করে।

15. **Fragments কী এবং কেন ব্যবহার হয়?**
    📌 React.Fragment (বা `<> </>`) ব্যবহার করা হয় multiple JSX element wrap করতে, DOM এ এক্সট্রা div না বাড়িয়ে।

---

## 🧩 Expert Level (দুর্দান্ত)

16. **Memoization কীভাবে Component এর জন্য কাজ করে?**
    📌 `React.memo()` দিয়ে functional component কে cache করা হয় যাতে props পরিবর্তন না হলে re-render না হয়।

17. **Key prop কেন দরকার হয় list render এ?**
    📌 প্রতিটি element কে identify করতে যাতে React efficiently re-render করতে পারে।

18. **Presentational vs Container Component কী?**
    📌 Presentational component UI দেখায়, Container component data এবং logic handle করে।

19. **Component Lifecycle কী?**
    📌 Component এর জন্ম থেকে ধ্বংস পর্যন্ত যে ধাপগুলো হয় — যেমন: `mount`, `update`, `unmount`।

20. **React Hook কি শুধুই functional component এ ব্যবহার করা যায়?**
    ✅ হ্যাঁ, React hook শুধু functional component এ ব্যবহৃত হয়।

---



