#### `forEach()`, `map()`, `filter()`, এবং `reduce()` এই চারটা জাভাস্ক্রিপ্ট অ্যারে মেথডকে ব্যাখ্যা :
---

## 🔍 1. `forEach()`

### 🔸 **What**:

`forEach()` হচ্ছে এমন একটা মেথড যা প্রতিটা অ্যারে এলিমেন্টের উপর একটা ফাংশন চালায়। কিন্তু **কিছু return করে না**।

### 🔸 **When to Use**:

যখন তুমি শুধু **কোনো কাজ করতে চাও**, যেমন কনসোলে দেখানো (`console.log()`), DOM ম্যানিপুলেশন বা অন্য অ্যাকশন, তখন `forEach()` ব্যবহার করো।

### 🔸 **How it Works**:

```js
array.forEach((element, index, array) => {
  // কাজ করো
});
```

### 🔸 উদাহরণ:

```js
const nums = [1, 2, 3];
nums.forEach((num) => {
  console.log(num * 2); // 2, 4, 6
});
```

### ⚙️ **Internal Work**:

* ভেতরে `for loop` এর মতো কাজ করে
* কিছু return করে না
* `break` বা `return` দিয়ে লুপ থামানো যায় না

### 🧠 **Execution Scope**:

* প্রতিটা iteration এ `element`, `index`, আর পুরো `array` পাবে
* কিন্তু loop থামাতে পারবে না

---

## 🔍 2. `map()`

### 🔸 **What**:

`map()` নতুন অ্যারে তৈরি করে যেটা পুরানো অ্যারেটার প্রতিটা এলিমেন্টকে **পরিবর্তন করে**।

### 🔸 **When to Use**:

যখন তুমি কোনো ডেটাকে **transform** বা **change** করতে চাও।

### 🔸 **How it Works**:

```js
const newArray = array.map((element, index, array) => {
  return element * 2;
});
```

### 🔸 উদাহরণ:

```js
const nums = [1, 2, 3];
const doubled = nums.map(num => num * 2);
console.log(doubled); // [2, 4, 6]
```

### ⚙️ **Internal Work**:

* নতুন অ্যারে return করে
* পুরানো অ্যারে বদলায় না

### 🧠 **Execution Scope**:

* প্রতিটা iteration এ ফাংশন চলে
* `return` ভ্যালুগুলো নতুন অ্যারেতে জমা হয়

---

## 🔍 3. `filter()`

### 🔸 **What**:

`filter()` এমন একটি মেথড যা এমন সব এলিমেন্ট রাখে যেগুলো একটি শর্ত **পাস করে**।

### 🔸 **When to Use**:

যখন তুমি ডেটা থেকে **কিছু বেছে নিতে চাও**, মানে condition-based সিলেকশন করতে চাও।

### 🔸 **How it Works**:

```js
const filteredArray = array.filter((element, index, array) => {
  return element > 2;
});
```

### 🔸 উদাহরণ:

```js
const nums = [1, 2, 3, 4];
const filtered = nums.filter(num => num > 2);
console.log(filtered); // [3, 4]
```

### ⚙️ **Internal Work**:

* ফাংশন চালায় প্রতিটা এলিমেন্টে
* `true` হলে এলিমেন্ট রাখে, `false` হলে বাদ দেয়

### 🧠 **Execution Scope**:

* ফাংশনের ভেতরে return করতে হয় `true/false`

---

## 🔍 4. `reduce()`

### 🔸 **What**:

`reduce()` হচ্ছে এমন একটা মেথড যা একটা অ্যারেকে **একটা মানে কমিয়ে আনে** (একটা সংখ্যা, অবজেক্ট, বা অ্যারে হতে পারে)।

### 🔸 **When to Use**:

যখন তুমি একটা **ফাইনাল রেজাল্ট** বের করতে চাও, যেমন টোটাল, গড়, গ্রুপিং ইত্যাদি।

### 🔸 **How it Works**:

```js
const result = array.reduce((accumulator, currentValue, index, array) => {
  return accumulator + currentValue;
}, initialValue);
```

### 🔸 উদাহরণ:

```js
const nums = [1, 2, 3];
const sum = nums.reduce((acc, num) => acc + num, 0);
console.log(sum); // 6
```

### ⚙️ **Internal Work**:

* `accumulator` আগে যা রেজাল্ট ছিল সেটা ধরে রাখে
* `currentValue` হচ্ছে বর্তমান এলিমেন্ট
* সব শেষে একটাই ভ্যালু return করে

### 🧠 **Execution Scope**:

* প্রতি স্টেপে আগের রেজাল্ট নিয়ে কাজ করে

---

## 🔁 Internal vs External Work টেবিল

| Function  | External Work (তুমি যা করো)   | Internal Work (JS যা করে)  |
| --------- | ----------------------------- | -------------------------- |
| `forEach` | side effects / একশন           | লুপ চালায়, রিটার্ন নাই     |
| `map`     | নতুন ভ্যালু return            | নতুন অ্যারে বানায়          |
| `filter`  | `true/false` return           | যেগুলো `true`, সেগুলো রাখে |
| `reduce`  | আগের মান + বর্তমান মান মেশানো | ফাইনাল একটা রেজাল্ট দেয়    |

---

## 🔥 Advanced Practice (উন্নত লেভেলের উদাহরণ)

### ✅ `forEach()`:

```js
const students = ['Salman', 'Fahim', 'Nashit'];
students.forEach((name, i) => console.log(`${i + 1}: ${name}`));
```

### ✅ `map()` + `filter()` একসাথে:

```js
const numbers = [1, 2, 3, 4, 5];
const doubledEvens = numbers
  .filter(num => num % 2 === 0)   // [2, 4]
  .map(num => num * 2);           // [4, 8]

console.log(doubledEvens); // [4, 8]
```

### ✅ `reduce()` দিয়ে গ্রুপিং:

```js
const people = [
  { name: 'Salman', age: 20 },
  { name: 'Rafi', age: 25 },
  { name: 'Tariq', age: 20 }
];

const groupedByAge = people.reduce((acc, person) => {
  acc[person.age] = acc[person.age] || [];
  acc[person.age].push(person.name);
  return acc;
}, {});

console.log(groupedByAge);
/*
{
  20: ['Salman', 'Tariq'],
  25: ['Rafi']
}
*/
```

---
অবশ্যই! নিচে তোমার দেওয়া সুন্দর comparison আর examples-এর ব্যাখ্যাটা আমি বাংলা ভাষায় **Step-by-step** ব্যাখ্যা করলাম, যেন একেবারে পরিষ্কারভাবে বুঝতে পারো।

---

## 📊 পার্ট ১: `forEach`, `map`, `filter`, এবং `reduce` — ভিজ্যুয়াল তুলনা (বাংলা ব্যাখ্যা সহ)

| ফিচার (Feature)       | `forEach()` (ফরইচ)                          | `map()` (ম্যাপ)                            | `filter()` (ফিল্টার)                              | `reduce()` (রিডিউস)                               |
| --------------------- | ------------------------------------------- | ------------------------------------------ | ------------------------------------------------- | ------------------------------------------------- |
| ✅ উদ্দেশ্য (Purpose)  | শুধু কিছু কাজ করা (লগ করা, পুশ করা)         | প্রতিটি এলিমেন্টকে নতুন করে রূপান্তর করা   | শর্ত অনুযায়ী কিছু এলিমেন্ট নির্বাচন করা           | সব এলিমেন্ট মিলে একটায় রূপান্তর (যেমন যোগফল)      |
| ✅ রিটার্ন করে কি?     | কিছুই না, `undefined`                       | নতুন অ্যারে (একই দৈর্ঘ্যের)                | নতুন অ্যারে (শর্ত পূরণকারী এলিমেন্টগুলো)          | একটি মান (যেকোনো টাইপ হতে পারে — সংখ্যা, অবজেক্ট) |
| ✅ মূল অ্যারে বদলায়?   | ❌ না                                        | ❌ না                                       | ❌ না                                              | ❌ না                                              |
| ✅ return দরকার কি?    | ❌ না (return দিলেও কিছু হয় না)              | ✅ হ্যাঁ, প্রতিটি আইটেম return করতে হয়      | ✅ হ্যাঁ, Boolean return করতে হয়                   | ✅ হ্যাঁ, accumulator return করতে হয়               |
| ✅ লুপ থামানো যায়?     | ❌ না                                        | ❌ না                                       | ❌ না                                              | ❌ না                                              |
| ✅ কোথায় ব্যবহার হয়?   | কনসোল লগ, DOM ম্যানিপুলেট, push করা ইত্যাদি | প্রতিটি আইটেমকে modify করতে (যেমন দ্বিগুণ) | condition অনুযায়ী এলিমেন্ট বাছাই (যেমন শুধু even) | সংখ্যা যোগফল, অবজেক্ট বানানো, কাউন্টিং ইত্যাদি    |
| ✅ কলব্যাক প্যারামিটার | `element`, `index`, `array`                 | `element`, `index`, `array`                | `element`, `index`, `array`                       | `accumulator`, `currentValue`, `index`, `array`   |

---

## 💡 পার্ট ২: ৩টি রিয়েল লাইফ এক্সাম্পল Line-by-Line বিশ্লেষণ সহ

---

### 🧪 উদাহরণ ১: প্রতিটি নাম্বারকে দ্বিগুণ করা

```js
const nums = [1, 2, 3];
```

| মেথড    | কোড                                                                             | আউটপুট      |
| ------- | ------------------------------------------------------------------------------- | ----------- |
| forEach | `let result = []; nums.forEach(n => result.push(n * 2));`                       | `[2, 4, 6]` |
| map     | `const result = nums.map(n => n * 2);`                                          | `[2, 4, 6]` |
| filter  | `const result = nums.filter(n => n * 2);` ❌ ভুলভাবে ব্যবহার                     | `[1, 2, 3]` |
| reduce  | `const result = nums.reduce((acc, n) => { acc.push(n * 2); return acc; }, []);` | `[2, 4, 6]` |

> **বিশ্লেষণ**:

* `map()` **সঠিক এবং আদর্শ** উপায় এমন রূপান্তরের জন্য।
* `forEach()` এবং `reduce()` দিয়েও করা যায়, তবে কোড বড় হয় এবং clean নয়।
* `filter()` এখানে **ভুলভাবে** ব্যবহৃত হয়েছে কারণ এটা মূলত ফিল্টার করার জন্য, রূপান্তরের জন্য নয়।

---

### 🧪 উদাহরণ ২: শুধু জোড় সংখ্যা (even numbers) রাখা

```js
const nums = [1, 2, 3, 4];
```

| মেথড    | কোড                                                                                          | আউটপুট               |
| ------- | -------------------------------------------------------------------------------------------- | -------------------- |
| forEach | `let result = []; nums.forEach(n => { if (n % 2 === 0) result.push(n); });`                  | `[2, 4]`             |
| map     | `const result = nums.map(n => n % 2 === 0 ? n : null);`                                      | `[null, 2, null, 4]` |
| filter  | `const result = nums.filter(n => n % 2 === 0);`                                              | `[2, 4]`             |
| reduce  | `const result = nums.reduce((acc, n) => { if (n % 2 === 0) acc.push(n); return acc; }, []);` | `[2, 4]`             |

> **বিশ্লেষণ**:

* `filter()` এখানে **সেরা উপায়** কারণ এটা শর্ত অনুযায়ী বাছাই করে।
* `map()` এর ভুল ব্যবহার এখানে `null` ফিরিয়ে দিচ্ছে।
* `forEach()` ও `reduce()` দিয়ে করা যায়, কিন্তু `filter()` সবচেয়ে পরিষ্কার ও শর্টকাট উপায়।

---

### 🧪 উদাহরণ ৩: সব সংখ্যার যোগফল বের করা

```js
const nums = [1, 2, 3, 4];
```

| মেথড    | কোড                                                | আউটপুট         |
| ------- | -------------------------------------------------- | -------------- |
| forEach | `let sum = 0; nums.forEach(n => sum += n);`        | `10`           |
| map     | `const result = nums.map(n => n);`                 | `[1, 2, 3, 4]` |
| filter  | `const result = nums.filter(n => n);`              | `[1, 2, 3, 4]` |
| reduce  | `const sum = nums.reduce((acc, n) => acc + n, 0);` | `10`           |

> **বিশ্লেষণ**:

* `reduce()` হলো **আদর্শ উপায়** যেকোনো "sum", "count", বা "object বানানো"-র জন্য।
* `forEach()` দিয়ে করা যায়, কিন্তু বাইরে ভ্যারিয়েবল লাগবে।
* `map()` এবং `filter()` এখানে **অপ্রয়োজনীয়**।

---

## ⚠️ সংক্ষিপ্ত টেবিল: কবে কোনটা ব্যবহার করবে?

| কাজ                        | সেরা মেথড   |
| -------------------------- | ----------- |
| array modify (রূপান্তর)    | `map()`     |
| শর্ত অনুযায়ী বাছাই         | `filter()`  |
| সব কিছু থেকে এক মান বানানো | `reduce()`  |
| শুধুমাত্র কিছু কাজ করা     | `forEach()` |

---

## 🧠 অতিরিক্ত টিপস (Bonus Tips in Bangla):

* সবসময় কোড লেখার আগে ভাবো — **"আমার দরকার কি?"**

  * নতুন অ্যারে দরকার? → `map()` / `filter()`
  * একটিমাত্র ফলাফল দরকার? → `reduce()`
  * শুধু console.log বা push করব? → `forEach()`
* মেথডগুলোর মধ্যে `map`, `filter`, `reduce` **চেইন করে** ব্যবহার করাও সম্ভব!

---
হ্যাঁ, `reduce()` মেথড ব্যবহার করার সময় **accumulator** অবশ্যই **return** করতে হয়। এটা `reduce()`-এর মূল কাজ করার জন্য অত্যন্ত গুরুত্বপূর্ণ।

চলো নিচের নিয়মমতো ব্যাখ্যা করি যেন সহজে বোঝো:

---

## 🧠 **What is `accumulator` in reduce()?**

`reduce()` ফাংশনের মধ্যে একটা callback ফাংশন চলে, যেখানে প্রতিবার চলার সময় আগের মান ধরে রাখার জন্য একটা ভেরিয়েবল লাগে। সেটাকেই বলে **accumulator**।

```js
array.reduce((accumulator, currentValue) => {
  return accumulator + currentValue;
}, initialValue);
```

---

## ⚠️ **Why must we `return` the accumulator?**

`reduce()` প্রতিবার callback চালানোর পর **accumulator**-এর নতুন মান জানতে চায়। যদি তুমি return না করো, তাহলে পরবর্তী ধাপে **undefined** হয়ে যাবে।

🔍 উদাহরণ:

```js
const nums = [1, 2, 3];

// ❌ Wrong: didn't return accumulator
const wrong = nums.reduce((acc, curr) => {
  acc += curr; // doing something
  // no return!
}, 0);

console.log(wrong); // ❌ undefined
```

✅ ঠিকভাবে করা:

```js
const nums = [1, 2, 3];

// ✅ Correct: returned accumulator
const correct = nums.reduce((acc, curr) => {
  acc += curr;
  return acc; // 🔁 return korte hobe
}, 0);

console.log(correct); // ✅ 6
```

---

## 🔁 Reduce এর Callback Step by Step

```js
const nums = [1, 2, 3, 4];

const result = nums.reduce((acc, curr, idx) => {
  console.log(`Step ${idx}: acc = ${acc}, curr = ${curr}`);
  return acc + curr;
}, 0);
```

Output হবে:

```
Step 0: acc = 0, curr = 1
Step 1: acc = 1, curr = 2
Step 2: acc = 3, curr = 3
Step 3: acc = 6, curr = 4
```

শেষে `result = 10`

---

## ✅ Summary (Bengali)

| জিনিস                 | ব্যাখ্যা                                                                 |
| --------------------- | ------------------------------------------------------------------------ |
| accumulator কী?       | আগের রিটার্ন করা মান যেটা পরের iteration এ carry হয়                      |
| return কেন জরুরি?     | কারণ return না করলে `accumulator` undefined হয়ে যাবে                     |
| কোথায় return করতে হয়? | reduce-এর callback ফাংশনের ভেতরে, প্রতিবার acc update করে return করতে হয় |

---


অবশ্যই ভাই! নিচে আমি বাংলা ভাষায় একদম beginner-friendly করে array destructuring আর spread operator-এর পূর্ণ ব্যাখ্যা দিয়েছি — যেন আপনি Junior Developer থেকেও এক ধাপ এগিয়ে যান।

---

## 🔶 পার্ট ১: Array Destructuring

### ✅ Array Destructuring কী?

Array destructuring হলো এমন একটা কৌশল যেখানে আমরা একটা অ্যারে থেকে একাধিক মান (value) একসাথে আলাদা আলাদা ভেরিয়েবল (variable) হিসেবে বের করে নিতে পারি।

🎯 ‍ সহজ ভাষায়:
👉 “index ধরে ধরে arr\[0], arr\[1] না লিখে এক লাইনেই সব ভ্যালু variable এ নিয়ে আসা।”

🧠 ধরুন:

```js
const arr = [10, 20, 30];
const [a, b, c] = arr;
console.log(a); // 10
console.log(b); // 20
```

এখানে automatically arr-এর প্রথম, দ্বিতীয়, তৃতীয় ভ্যালু a, b, c এর মধ্যে ঢুকে গেছে।

---

### 🔍 কখন ব্যবহার করবো?

✅ যখন অ্যারে থেকে specific মানগুলো লাগবে
✅ যখন function একটা array রিটার্ন করে
✅ React এ useState hook ব্যাবহার করার সময়
✅ মান পরিবর্তনের সময় (Swap values)
✅ একাধিক ভেরিয়েবলে মান রাখার প্রয়োজন হলে

---

### ⚙️ ভিতরের কাজের ধরন (Logic):

Destructuring মূলত অ্যারে-এর index অনুযায়ী কাজ করে।
যেমনঃ

```js
const nums = [100, 200];
const [x, y] = nums;
// x = nums[0], y = nums[1]
```

👉 position match করে মান বসিয়ে দেয়।

---

### ✨ Extra সুবিধা (Advanced but easy):

1. ‍⏭️ কোনো value skip করা যায়:

```js
const [a, , c] = [1, 2, 3];
console.log(c); // 3
```

2. ✅ Default value দেওয়া যায়:

```js
const [x = 5, y = 10] = [1];
console.log(y); // 10
```

3. 🔁 মান পরিবর্তন (Swap two variables):

```js
let a = 1, b = 2;
[a, b] = [b, a];
console.log(a, b); // 2, 1
```

4. 🧩 Nested destructuring:

```js
const arr = [1, [2, 3]];
const [x, [y, z]] = arr;
console.log(y); // 2
```

---

## 🧪 Array Destructuring এর ৩টি উদাহরণ:

✅ Example 1:

```js
const studentMarks = [90, 85, 88];
const [math, physics, chemistry] = studentMarks;
console.log(math); // 90
```

✅ Example 2:

```js
function getNameAndAge() {
  return ['Salman', 21];
}

const [name, age] = getNameAndAge();
console.log(name, age); // Salman 21
```

✅ Example 3 (React style):

```js
const [count, setCount] = useState(0);
```

---

## 🔷 পার্ট ২: Spread Operator (...)

### ✅ Spread Operator কী?

👉 ‍Spread operator হলো তিনটি dot (...) দিয়ে বানানো একটি শক্তিশালী টুল যা array/object এর ভেতরের সব item আলাদা করে "প্রসারিত" (spread) করে দেয়।

🎯 সহজভাবে:
👉 পুরনো অ্যারে কপি করতে বা একাধিক অ্যারে একসাথে জোড়া লাগাতে ‍... ব্যবহার করা হয়।

---

### 🔍 কখন ব্যবহার করবো?

✅ একটা অ্যারে কপি করতে
✅ দুইটা অ্যারে merge করতে
✅ function এ multiple value পাঠাতে
✅ Object-এর copy তৈরি করতে
✅ রিএক্ট-এ props পাঠানোর সময়

---

### 🧠 ভিতরের কাজের ধরন:

Spread operator একটা অ্যারে বা অবজেক্ট কে ভেঙে individual item বানিয়ে দেয়। যেমনঃ

```js
const arr = [1, 2, 3];
console.log(...arr); // 1 2 3
```

---

### ✨ তুলনা: Spread vs Normal Copy

| Traditional Copy       | Spread Operator         |
| ---------------------- | ----------------------- |
| for loop বা manual way | \[...array] দিয়ে কপি হয় |
| কোড বড় হয়             | এক লাইনে শেষ            |
| কম efficient           | clean ও fast            |

---

## 🧪 Spread Operator এর ৩টি উদাহরণ:

✅ Example 1: অ্যারে কপি

```js
const numbers = [10, 20, 30];
const copied = [...numbers];
console.log(copied); // [10, 20, 30]
```

✅ Example 2: অ্যারে Merge

```js
const a = [1, 2];
const b = [3, 4];
const merged = [...a, ...b];
console.log(merged); // [1, 2, 3, 4]
```

✅ Example 3: Function এ ভ্যালু পাঠানো

```js
function sum(x, y, z) {
  return x + y + z;
}

const values = [5, 10, 15];
console.log(sum(...values)); // 30
```

---

## 🔁 Bonus: Rest vs Spread Operator

দুটো দেখতে একই (...), কিন্তু কাজ আলাদা:

| Spread Operator                      | Rest Parameter                      |
| ------------------------------------ | ----------------------------------- |
| \[...arr] (break into parts)         | (...args) (gather into array)       |
| array/object এর ভেতরের মান বাইরে নেয় | Function এ অনেক argument নেয়ার জন্য |

🔄 উদাহরণ:

```js
// Spread
const arr = [1, 2, 3];
const copy = [...arr];

// Rest
function printAll(...args) {
  console.log(args); // array of all args
}
```

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
const arr2 = \[10, 30];
const merged = \[...arr1, ...arr2];
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

—

Bonus Tips for Mastery:

* destructuring ও spread operator শুধু array না, object এর সাথেও কাজ করে। পরে আমরা object destructuring & rest/spread নিয়ে চ্যালেঞ্জ করব।
* আপনি প্রতিটি কোড নিজে run করুন VS Code বা browser console এ।
* ভুল হলে console.log দিয়ে দেখুন কোন ভ্যারিয়েবলে কী আসছে।

আপনি চাইলে Challenge 6–10 (object ভিত্তিক destructuring & spread) নিয়ে এগিয়ে যেতে পারেন।


