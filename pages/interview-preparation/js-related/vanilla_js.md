<div align='center'>

# JavaScript Interview Question
</div>

## 📚 Table of Contents

1. [What is the Higher Order function & callback function in JavaScript?]()
1. [What is Hoisting & closure in JavaScript?]()
1. [What is Scope in javascript?]()
1. [What is the difference between Call, Apply, and Bind?]()
1. [What is the difference between undefined and null ?]()
1. [What is a cookie?]()
1. [What is a promise ?]()
1. [What is an event loop? How does javaScript handle asynchronous tasks?]()
1. [What is a prototype chain ?]()
1. [How can you eliminate duplicate values from a JavaScript array?]()

<br>



## 1️⃣ Higher Order Function & Callback Function কী?

**Higher Order Function**
যে ফাংশন অন্য একটি ফাংশনকে **parameter হিসেবে নেয়** অথবা **return করে**, তাকে Higher Order Function বলে।
👉 উদাহরণ: `map()`, `filter()`, `reduce()`

**Callback Function**
যে ফাংশনকে অন্য ফাংশনের ভিতরে **argument হিসেবে পাঠানো হয়** এবং পরে কল করা হয়, সেটাই Callback Function।

**সহজভাবে:**

> ফাংশন যদি ফাংশনের সাথে কাজ করে → Higher Order
> যে ফাংশন পাঠানো হয় → Callback

---

## 2️⃣ Hoisting & Closure কী?

### 🔹 Hoisting

JavaScript কোড রান করার আগে **variable ও function declaration উপরে তুলে নেয়**—এটাই Hoisting।

* `var` hoist হয় (undefined থাকে)
* `let` ও `const` hoist হয় কিন্তু ব্যবহার করা যায় না (TDZ)

### 🔹 Closure

যখন একটি inner function তার outer function-এর variable **মনে রাখতে পারে**, even outer function শেষ হয়ে গেলেও—এটাই Closure।

**সহজভাবে:**

> Closure = function + তার বাইরের data মনে রাখা

---

## 3️⃣ Scope কী?

**Scope** মানে হলো—কোথা থেকে কোন variable অ্যাক্সেস করা যাবে।

### Types:

* **Global Scope** – সব জায়গা থেকে পাওয়া যায়
* **Function Scope** – শুধু function এর ভিতরে
* **Block Scope** – `{ }` এর ভিতরে (`let`, `const`)

---

## 4️⃣ Call, Apply, Bind এর পার্থক্য কী?

সবগুলোই function এর `this` সেট করতে ব্যবহার হয়।

* **call()** → argument আলাদা আলাদা
* **apply()** → argument array আকারে
* **bind()** → সাথে সাথে call হয় না, নতুন function return করে

**সহজভাবে:**

> call = এখনই, আলাদা argument
> apply = এখনই, array argument
> bind = পরে call করার জন্য

---

## 5️⃣ undefined ও null এর পার্থক্য কী?

* **undefined**
  Variable আছে কিন্তু কোনো value দেওয়া হয়নি
* **null**
  ইচ্ছা করে empty value দেওয়া হয়েছে

👉 `undefined` → system দেয় <br>
👉 `null` → developer দেয়

---

## 6️⃣ Cookie কী?

**Cookie** হলো ছোট data যা browser-এ save থাকে।

👉 ব্যবহার হয়:

* login session
* user preference
* tracking

👉 cookie client-side এ থাকে এবং server এ পাঠানো হয়

---

## 7️⃣ Promise কী?

**Promise** হলো asynchronous কাজ handle করার একটি উপায়।

Promise-এর ৩টি state:

* **pending** – কাজ চলছে
* **fulfilled** – সফল
* **rejected** – ব্যর্থ

👉 `then()` → success
👉 `catch()` → error

---

## 8️⃣ Event Loop কী? JavaScript async কাজ কীভাবে handle করে?

JavaScript **single-threaded**, মানে একসাথে একটাই কাজ করে।

**Event Loop**:

* Call Stack দেখে
* Task Queue / Microtask Queue থেকে কাজ নেয়
* Stack ফাঁকা হলে async কাজ চালায়

**সহজভাবে:**

> Event Loop ঠিক করে কখন কোন async কাজ চালু হবে

---

## 9️⃣ Prototype Chain কী?

JavaScript-এ object অন্য object থেকে property inherit করে **prototype-এর মাধ্যমে**।

যদি কোনো property object-এ না পাওয়া যায় → <br>
👉 prototype এ খোঁজে <br>
👉 তারপর prototype-এর prototype এ (chain)

এটাই **Prototype Chain**

---

## 🔟 JavaScript Array থেকে duplicate value কীভাবে remove করবেন?

### সবচেয়ে common উপায়:

```js
const uniqueArray = [...new Set(array)];
```

👉 `Set` duplicate নেয় না <br>
👉 আবার array বানিয়ে ফেলি

---

### 🔚 ইন্টারভিউ টিপস

এই উত্তরগুলো **clear, short এবং confident** ভাবে বললে ভালো impression পড়ে।

চাও তো আমি এগুলো:

* **১ লাইনের short answer**
* **code example সহ**
* **mock interview Q&A format**

এও বানিয়ে দিতে পারি।
