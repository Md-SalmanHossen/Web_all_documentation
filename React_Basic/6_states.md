
## 🟢 STATE: Data maintained inside a component

### 🔹 What it is:

State হলো component-এর ভিতরের এক ধরনের storage যেটা dynamically change হতে পারে। এটি interactive component এর জন্য সবচেয়ে important।

### 🔹 কিভাবে কাজ করে:

1. State define হয় useState() hook দিয়ে
2. State change হলে component automatically re-render হয়
3. State use হয় mostly user interaction handle করতে

📦 উদাহরণ:

```jsx
import { useState } from 'react';

function ClickCounter() {
  const [count, setCount] = useState(0); // state initialize

  const handleClick = () => {
    setCount(count + 1); // state update
  }

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={handleClick}>Click me</button>
    </div>
  );
}
```

👉 এখানে count হলো state, আর setCount হলো সেই state update করার function। যেই মুহূর্তে তুমি state change করো — React নিজে নিজে component টা রি-render করে।

### 🔸 State এর বৈশিষ্ট্য:

| Feature         | Description                                   |
| --------------- | --------------------------------------------- |
| Scope           | Component এর ভিতরে                            |
| Change allowed? | হ্যাঁ, useState/setState দিয়ে                 |
| Trigger Render? | হ্যাঁ                                         |
| Use Cases       | UI Interaction, Dynamic Data, Forms etc       |
| Example         | const \[data, setData] = useState(initialVal) |

---
