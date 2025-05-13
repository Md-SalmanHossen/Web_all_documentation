# 🚀 React Component Thinking Master Guide 

## 🔥 3টি Core চিন্তা – Components নিয়ে কাজ করার সময়:

✅ **Component গুলো কিভাবে চিন্তা করতে হবে**
✅ **State কোথায় থাকবে সেটা ঠিক করতে হবে**
✅ **Data কোন দিক থেকে যাবে সেটা বুঝতে হবে**

---

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
অবশ্যই! এখন আমরা যাবো **Part 2** তে — "State কোথায় থাকবে সেটা ঠিক করতে হবে", অর্থাৎ **Where to Put State in React**। এইটা React component design-এর second most important চিন্তা।

---

# ⚙️ Part 2: Where to Put State – The Right Way

React বলেই দিয়েছে:

> **"Lift the state up when multiple components need access."**

তাহলে প্রশ্ন আসে...

---

## 🧠 Step-by-Step চিন্তা: State কোথায় রাখব?

### 🔹 Step 1: কে এই data/useState টা ইউজ করছে?

* শুধু একটা component ইউজ করছে?
  👉 ওই component-এই state রাখো।

* একাধিক sibling component ইউজ করছে?
  👉 **common parent** এ state রাখো (lift state up)।

---

### 🔹 Step 2: Static নাকি Dynamic?

* যদি data টা change না হয় = static
  👉 props দিয়ে পাঠাও

* যদি data change হয় + UI reflect করে
  👉 state দিয়ে রাখো (useState/useReducer)

---

### 🔹 Step 3: Direction of Data Flow বুঝো

React এ data সবসময়:

> **"Top to bottom (Parent → Child)"**

🔄 যদি child থেকে parent কে data জানাতে চাও, তখন:

👉 **callback function props দিয়ে পাঠাও**

```jsx
<Child onUpdate={handleUpdate} />
```

---

## ✅ Rules of State Placement – Table

| Scenario                            | State রাখা উচিত                     |
| ----------------------------------- | ----------------------------------- |
| শুধু একটা component ইউজ করছে        | ওই component-এর ভিতর                |
| দুই sibling ইউজ করছে                | তাদের common parent-এ               |
| global app এর অনেক জায়গায় ইউজ হচ্ছে | Context API বা Redux (global state) |
| child update করে parent কে জানায়    | callback দিয়ে update trigger করানো  |

---

## 🔂 Example: Lift State Up

### ❌ ভুল ধরন:

```jsx
// Parent.jsx
<ProductCard />
<CartSidebar />
```

দুটোই নিজের ভিতরে state রাখছে।

### ✅ সঠিক ধরন:

```jsx
// Parent.jsx
const [cartItems, setCartItems] = useState([]);
return (
  <>
    <ProductCard onAddToCart={(item) => setCartItems([...cartItems, item])} />
    <CartSidebar cartItems={cartItems} />
  </>
);
```

---

## 📦 Component State Decision Tree

```
          +----------------------------+
          | Does it change over time? |
          +-----------+----------------
                      |
             No       |     Yes
            (props)   |  
                      ↓
            Is it needed by others?
                |         |
              No          Yes
         (Keep local)   (Lift up)
```

---

## 🌐 Global State কখন লাগবে?

যখন...

* Auth info (logged in user)
* Theme (dark/light)
* Language
* Cart items (e-commerce)
* Notifications

তখন তুমি `React Context` বা `Redux` বা `Zustand` ইউজ করতে পারো।

---

## 🔚 Final Summary – State Placement

* ✅ Only you? → local state
* 🔄 Two or more? → lift up
* 🌐 Everyone? → context / redux
* 📤 From child → use callbacks

---


# ⚙️ Part 3: Data কোন দিক থেকে যাবে সেটা বুঝতে হবে – Direction of Data Flow

React-এ data flow শুধু একদিকে হয়: **top to bottom** অর্থাৎ Parent থেকে Child। তবে, Data কিভাবে যাবে তা design করতে কিছু fundamental নিয়ম এবং patterns আছে। চল, সেইগুলো দেখি।

---

## 🧠 Step-by-Step চিন্তা: Data Flow ঠিকভাবে বুঝতে হবে

### 🔹 Step 1: Data Flow Basics

React-এ data flow হয় একদম top থেকে bottom, অর্থাৎ Parent component থেকে Child component। Parent তার state বা props এর মাধ্যমে Child কে data পাঠায়। কিন্তু Child থেকে Parent কে data পাঠানোর জন্য আমরা **callback functions** ব্যবহার করি।

---

### 🔹 Step 2: Unidirectional Data Flow

**Unidirectional Data Flow** মানে, data সবসময় **Parent → Child** যায়, কখনোই **Child → Parent** না। React এ data flow এই rule মেনে চলে:

* **State** থাকে Parent এর মধ্যে (যদি Multiple components ওই state কে access করে)।
* **Props** ব্যবহার করে Parent তার state Child এ পাঠায়।

---

### 🔹 Step 3: Child থেকে Parent Data পাঠানোর উপায়

যখন Child থেকে Parent কে data পাঠাতে হয়, তখন **callback functions** ব্যবহার করতে হবে। Child component তার data **callback function**-এ pass করবে, আর Parent সেই data টা ব্যবহার করবে।

```jsx
// Parent.jsx
const Parent = () => {
  const [value, setValue] = useState('');

  const handleChange = (newValue) => {
    setValue(newValue); // update parent state with child data
  };

  return (
    <div>
      <Child onChange={handleChange} />
      <p>Data from child: {value}</p>
    </div>
  );
};

const Child = ({ onChange }) => {
  return (
    <button onClick={() => onChange('New data from child!')}>
      Send Data to Parent
    </button>
  );
};
```

এই কোডে:

* `Parent` component একটা state রাখছে।
* `Child` component একটা button ক্লিক করলে `Parent`-এর `handleChange` function call হবে।

---

### 🔹 Step 4: Prop Drilling – Multiple Levels of Props

**Prop Drilling** হল যখন অনেক level গভীর পর্যন্ত props পাঠাতে হয়। উদাহরণস্বরূপ, যদি তুমি data from Parent → Child → Grandchild পাঠাতে চাও।

```jsx
const Parent = () => {
  const [message, setMessage] = useState("Hello from Parent!");

  return <Child message={message} />;
};

const Child = ({ message }) => {
  return <GrandChild message={message} />;
};

const GrandChild = ({ message }) => {
  return <p>{message}</p>;
};
```

এই ক্ষেত্রে, data flow হচ্ছে `Parent -> Child -> GrandChild`। যদি data বেশি level গভীর হতে থাকে, তবে prop drilling কষ্টকর হতে পারে। এর জন্য **Context API** বা **Redux** ব্যবহারের কথা ভাবা উচিত।

---

## 🛠️ How to Avoid Prop Drilling

### 🔹 Context API:

যখন একই data একাধিক components এ প্রয়োজন, তখন **Context API** ব্যবহার করে global state setup করতে পারো। Context API দিয়ে, তুমি Parent থেকে Child তে props পাঠানোর ঝামেলা থেকে মুক্তি পাবে।

```jsx
const MyContext = createContext();

const Parent = () => {
  const [message, setMessage] = useState("Hello from Parent!");

  return (
    <MyContext.Provider value={message}>
      <Child />
    </MyContext.Provider>
  );
};

const Child = () => {
  return <GrandChild />;
};

const GrandChild = () => {
  const message = useContext(MyContext);
  return <p>{message}</p>;
};
```

এখানে `MyContext.Provider` Parent component-এ wrap করা হচ্ছে, আর Child এবং GrandChild components `useContext` hook দিয়ে Context value access করছে।

---

## 🌐 Global State Patterns

### 🔹 Redux:

যদি data global level এ manage করতে হয়, Redux বা অন্য কোনো state management library ব্যবহার করা উত্তম। Redux এ global state setup করতে পারো, এবং কোনো level এর component থেকে data access বা update করা সহজ হয়।

---

## 🚀 Data Flow & Design Pattern Recap

### ✅ Rules of Data Flow:

* **One-way data flow**: Data গুলো সবসময় **Parent → Child** যাবে।
* **Child → Parent**: Callback function pass করো, data কে handle করতে।
* **Avoid prop drilling**: **Context API** বা **Redux** ব্যবহার করো।

---

## 📦 Data Flow Decision Tree

```
        +---------------------+
        | Need shared data?   |
        +-----------+---------+
                    |
                Yes | No
                    |
        +-----------+---------+
        | Context API or Redux|
        +---------------------+
        | Prop Drilling       |
        +---------------------+
```

---

## 🔚 Final Summary – Data Flow

* **Data always flows from top to bottom**: Parent → Child
* **Child to Parent**: Use callback functions.
* **Avoid prop drilling**: Use Context API/Redux for global state.

---



