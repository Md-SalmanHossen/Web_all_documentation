## 🔍 Rest Operator কি?

**Rest Operator (`...`)** ব্যবহার করা হয় **multiple values** কে **একটা variable এ "gather" বা "ধরার" জন্য।**

🔁 মনে রাখো:

* `spread` = **values কে ভেঙে ছড়িয়ে দেওয়া**
* `rest` = **values কে জড়ো করে একটি variable-এ রাখা**

---

## ✅ Basic Syntax:

```js
const [a, ...rest] = [1, 2, 3, 4];
// a = 1, rest = [2, 3, 4]
```

---

## 🧠 Rest Operator কোথায় কোথায় ব্যবহার হয়?

---

## ✅ ১. **Array Destructuring-এ ব্যবহার**

```js
const numbers = [10, 20, 30, 40];
const [first, second, ...rest] = numbers;

console.log(first);  // 10
console.log(second); // 20
console.log(rest);   // [30, 40]
```

🔍 **ব্যাখ্যা**:
`first` ও `second` আলাদা করে নিচ্ছি, বাকি সব `rest` array-তে চলে গেছে।

---

## ✅ ২. **Function Parameters-এ Rest Parameter**

যখন function-এ নির্দিষ্ট কিছু parameter থাকলেও আমরা চাই অতিরিক্ত যত argument পাঠানো হবে সব এক variable-এ ধরতে:

```js
function sum(...nums) {
  return nums.reduce((total, n) => total + n, 0);
}

console.log(sum(1, 2));         // 3
console.log(sum(5, 10, 20));    // 35
```

🔍 **ব্যাখ্যা**:

* `...nums` → সব arguments কে array হিসেবে ধরে
* `reduce` দিয়ে যোগ করে return করছে

---

## ✅ ৩. **Object Destructuring-এ ব্যবহার**

```js
const person = {
  name: "John",
  age: 30,
  city: "New York",
  profession: "Engineer"
};

const { name, ...rest } = person;

console.log(name); // John
console.log(rest); // { age: 30, city: "New York", profession: "Engineer" }
```

🔍 **ব্যাখ্যা**:
`name` আলাদা করে নিলাম, আর বাকি সব property `rest` object-এ।

---

## ✅ ৪. **React Component Parameters-এ ব্যবহার**

```jsx
function Button({ children, ...props }) {
  return <button {...props}>{children}</button>;
}

<Button onClick={() => alert("Hi")} className="btn">Click</Button>
```

🔍 **ব্যাখ্যা**:

* `children` আলাদা করে নিচ্ছি
* বাকি props যেমন `onClick`, `className` সব `...props` দিয়ে button-এ spread করছি

---

## 🧠 Spread vs Rest Operator (ভুল কোরো না!)

| Feature        | Spread Operator              | Rest Operator                 |
| -------------- | ---------------------------- | ----------------------------- |
| কাজ কী?        | ভেঙে ফেলে                    | জড়ো করে (gather করে)          |
| কোথায় ব্যবহার? | Function call, props passing | Function param, destructuring |
| Array/Object   | ভেঙে দেয়                     | ধরে রাখে                      |

---

## 🔚 উপসংহার

**Rest Operator (`...`)**:

* Function param-এ multiple arguments ধরতে কাজে লাগে
* Array/Object destructuring-এ বাকি মান ধরে রাখে
* React Component-এ common props ধরার জন্য দারুণ

---




## ✅ More Details **React Component Parameters-এ rest operator**

### 🔍 কী কাজ করে?

👉 Function parameter এ `{ ...rest }` ব্যবহার করলে আমরা **বাকি সব props (property)** গুলো ধরতে পারি যেগুলো destructure করে আলাদা করিনি।

---

### 📌 Basic Syntax:

```jsx
function MyComponent({ knownProp1, knownProp2, ...rest }) {
  // knownProp1, knownProp2 আলাদা করেছি
  // ...rest → বাকি props ধরেছে
}
```

---

## 🧠 কেন ব্যবহার করি?

✅ অনেক সময় একটা Component এ multiple props পাঠানো হয়।
✅ সবগুলো আলাদা করে না নিয়ে শুধু কিছু important props নিই, বাকি সব `rest` দিয়ে ধরে নিই।
✅ এই `rest` কে আমরা child component বা HTML element এ spread করে দিতে পারি।

---

## 🔰 উদাহরণ ১: Button Component (Reusable)

```jsx
function MyButton({ children, className, ...rest }) {
  return (
    <button className={`btn ${className}`} {...rest}>
      {children}
    </button>
  );
}
```

### 👉 যখন ব্যবহার করবো:

```jsx
<MyButton onClick={() => alert("Clicked!")} type="submit" className="primary">
  Submit
</MyButton>
```

#### ⚙️ এখানে কী হচ্ছে?

| Code Part            | কাজ                                   |
| -------------------- | ------------------------------------- |
| `className`          | manually destructure করেছি            |
| `...rest`            | onClick, type এগুলো ধরে রেখেছে        |
| `<button {...rest}>` | ওগুলোকে ছড়িয়ে দিচ্ছে button element-এ |

---

## 🔰 উদাহরণ ২: Input Field Component

```jsx
function InputField({ label, name, ...rest }) {
  return (
    <div className="input-group">
      <label htmlFor={name}>{label}</label>
      <input id={name} name={name} {...rest} />
    </div>
  );
}
```

### 👉 যখন ব্যবহার করবো:

```jsx
<InputField
  label="Username"
  name="username"
  type="text"
  placeholder="Enter your name"
  onChange={handleChange}
/>
```

#### ⚙️ ব্যাখ্যা:

* label, name → আলাদা করে নিয়েছি
* type, placeholder, onChange → `...rest` এর মধ্যে capture হয়েছে
* সেগুলো `<input {...rest}>` এ spread হয়ে গিয়েছে

---

## 🔍 কী ধরণের props `rest`-এ পড়ে?

* `onClick`, `type`, `placeholder`, `value`, `disabled`, `id`, `style`, etc.
* এমনকি custom props (যেমন `data-testid`) ও `rest` এর মধ্যে পড়ে।

---

## ✅ উপকারিতা (Advantages):

| সুবিধা          | ব্যাখ্যা                                     |
| --------------- | -------------------------------------------- |
| Clean code      | সব prop destructure না করে সহজে ধরা যায়      |
| Reusability     | generic component বানাতে সাহায্য করে         |
| Flexibility     | নতুন prop এড করলে কোড পরিবর্তনের দরকার হয় না |
| Maintainability | সহজে changes handle করা যায়                  |

---

## 🚫 কখন `rest` না ব্যবহার করাই ভালো?

| অবস্থা                                    | কেন?                                         |
| ----------------------------------------- | -------------------------------------------- |
| component-এ specific props limit করতে চাও | যেন কেউ ভুলভাবে অতিরিক্ত prop না দেয়         |
| security/privacy reason                   | যদি কিছু sensitive prop ভুল করে pass হয়ে যায় |

---

## 🔚 সংক্ষিপ্ত রিভিউ:

### 🔑 Rule:

```jsx
function Component({ known, ...rest }) {
  // rest contains the rest of the props
}
```

### 🔧 Spread করে দিলে:

```jsx
<element {...rest} />
```

### 🧪 কাজ করে:

* Reusable Components (Button, Input, Card, etc.)
* Higher Order Components
* Form Handling
* Third-party component wrapper

---



✅ Challenge 1: Basic Destructuring & Sum

Task:
const numbers = \[5, 10, 15, 20];
এই অ্যারে থেকে প্রথম ৩টি মান নিয়ে যোগফল বের করতে হবে।

Solution:

```const numbers = \[5, 10, 15, 20];
const \[a, b, c] = numbers;
const sum = a + b + c;
console.log("Sum is:", sum);
```
Explanation:

* const \[a, b, c] = numbers; এখানে array destructuring করে numbers অ্যারের প্রথম তিনটি মান আলাদা করে নিচ্ছি।
* a = 5, b = 10, c = 15
* এরপর আমরা sum বের করি → 5 + 10 + 15 = 30

Output:
Sum is: 30

---

✅ Challenge 2: Swap Two Numbers Using Destructuring

Task:
let x = 7, y = 3;
এখন এই দুই ভেরিয়েবলের মান পরিবর্তন করতে হবে।

Solution:
```
let x = 7;
let y = 3;
\[x, y] = \[y, x];
console.log("x =", x);
console.log("y =", y);
```
Explanation:

* আগের দিনে swap করতে হলে temp variable লাগত, কিন্তু এখন এক লাইনে করা যায়।
* এখানে \[x, y] = \[y, x] মানে হচ্ছে: x-তে y-এর মান যাবে, আর y-তে x-এর মান যাবে।

Output:
x = 3
y = 7

---

✅ Challenge 3: Spread Operator দিয়ে Merge এবং Sort

Task:
const arr1 = \[40, 60];
const arr2 = \[10, 30];
এই দুইটা অ্যারে merge করে sort করতে হবে।

Solution:

```const arr1 = \[40, 60];
const arr2 = [10, 30];
const merged = [...arr1, ...arr2];
const sorted = merged.sort((a, b) => a - b);
console.log(sorted);
```
Explanation:

* \[...arr1, ...arr2] → এটি spread operator ব্যবহার করে দুটি অ্যারেকে একসাথে merge করে।
* sort((a, b) => a - b) → এটি ascending order-এ sort করে (নাম্বার হিসেবে)। JavaScript এ .sort() ডিফল্টভাবে string হিসেবে sort করে, তাই কম্পেয়ার ফাংশন ব্যবহার করা হয়েছে।

Output:
\[10, 30, 40, 60]

---

✅ Challenge 4: Function থেকে Array Return → Destructure

Task:
একটি ফাংশন লিখুন যেটি return করবে → \['React', 'Vue', 'Angular'] এবং প্রথম ও শেষ উপাদান destructure করুন।

Solution:
```
function getFrameworks() {
return \['React', 'Vue', 'Angular'];
}

const \[first, , last] = getFrameworks();

console.log("first =", first);
console.log("last =", last);
```
Explanation:

* ফাংশন getFrameworks() অ্যারে রিটার্ন করে।
* আমরা first এবং last কে destructure করেছি, মাঝেরটা (Vue) বাদ দিয়েছি।
* , দিয়ে index skip করা হয়।

Output:
first = React
last = Angular

---

✅ Challenge 5: Function Arguments → Spread করে Pass করুন

Task:
data অ্যারে আছে → \[4, 5, 6]
sum(x, y, z) ফাংশনে spread করে এই তিনটি মান পাঠান।

Solution:
```
function sum(x, y, z) {
return x + y + z;
}

const data = \[4, 5, 6];
const result = sum(...data);
console.log("Result is:", result);
```
Explanation:

* sum ফাংশন তিনটি parameter নেয়।
* আমরা data অ্যারেকে ...data দিয়ে spread করেছি, যার মানে → sum(4, 5, 6)
* তারপর যোগফল রিটার্ন করে।

Output:
Result is: 15

#### **rest, spread, destructure** এর মধ্যে পার্থক্য ব্যাখ্যা করেছি একটা সুন্দর **📊 টেবিল** এবং **🧪 এক্সাম্পল** দিয়ে, যাতে একবারেই বুঝে ফেলা যায়।


##### 📊 তুলনামূলক টেবিল: `Destructuring vs Spread vs Rest`

| ফিচার             | কাজ/উদ্দেশ্য                                   | সিনট্যাক্স                             | ব্যবহার কোথায় হয়                     | Key দিক             |
| ----------------- | ---------------------------------------------- | -------------------------------------- | ------------------------------------ | ------------------- |
| **Destructuring** | Object/Array থেকে value বের করা                | `const {a} = obj` or `const [x] = arr` | Variable declare করার সময়            | সরাসরি value access |
| **Spread**        | একটি Object/Array এর সবকিছু কপি বা ছড়িয়ে দেওয়া | `{...obj}` or `[...arr]`               | Props pass, clone/copy               | জিনিস "ছড়িয়ে" দেয়   |
| **Rest**          | বাকি (unpicked) মানগুলো ধরার জন্য              | `...rest`                              | Function param বা destructure এর সময় | বাকি সব জমা করে     |

---

## 🧪 একই Example দিয়ে তিনটা বুঝি:

### ⛳ Input Object:

```js
const user = {
  name: "Alice",
  age: 25,
  city: "Dhaka"
};
```

---

### ✅ 1. **Destructuring** (Object থেকে মান বের করা)

```js
const { name, age } = user;

console.log(name); // Alice
console.log(age);  // 25
```

> শুধু `name` ও `age` আলাদা করে বের করেছি।

---

### ✅ 2. **Rest Operator** (বাকি মান জমা রাখা)

```js
const { name, ...rest } = user;

console.log(name); // Alice
console.log(rest); // { age: 25, city: "Dhaka" }
```

> `name` বাদে যেটা ছিলো (মানে `age` ও `city`) সেগুলো `rest` নামে object হয়ে গেছে।

---

### ✅ 3. **Spread Operator** (object ছড়িয়ে দেওয়া)

```js
const clone = { ...user, country: "Bangladesh" };

console.log(clone);
/*
{
  name: "Alice",
  age: 25,
  city: "Dhaka",
  country: "Bangladesh"
}
*/
```

> পুরো `user` object কে spread করে নতুন property add করলাম `country`।

---

## ⚛️ React Example (একসাথে তিনটা):

```jsx
function Profile({ name, age, ...rest }) {
  return (
    <div {...rest}>
      <h2>{name}</h2>
      <p>Age: {age}</p>
    </div>
  );
}
```

```jsx
<Profile
  name="Alice"
  age={25}
  id="user-profile"
  className="card"
/>
```

### ব্যাখ্যা:

| কাজ                      | ব্যাখ্যা                                              |
| ------------------------ | ----------------------------------------------------- |
| `{ name, age, ...rest }` | 👉 Destructuring + Rest operator                      |
| `...rest`                | 👉 `id`, `className` spread হয়ে `<div>` এ apply হচ্ছে |
| `<div {...rest}>`        | 👉 Spread operator দিয়ে বাকি props ছড়ানো হচ্ছে        |

---

### ✅ সংক্ষেপে মনে রাখার ট্রিকস:

| কী                | মনে রাখার টিপ                          |
| ----------------- | -------------------------------------- |
| **Destructuring** | 👉 বাক্স থেকে জিনিস বের করে আনো        |
| **Rest**          | 👉 না বের করা বাকী জিনিস একজায়গায় জমাও |
| **Spread**        | 👉 জমা জিনিস আবার ছড়িয়ে দাও            |







