#### `forEach()`, `map()`, `filter()`, এবং `reduce()` এই চারটা জাভাস্ক্রিপ্ট অ্যারে মেথড ব্যাখ্যা :
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
