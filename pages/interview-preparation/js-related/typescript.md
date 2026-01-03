<div align='center'>

# TypeScript  Interview Question
</div>

## 📚 Table of Contents

1. [What are the three main primitive data types in TypeScript?]()
1. [What is an Interface in typescript?]()
1. [What is a type assertion in typescript?]()
1. [How many access modifiers are there in typeScript?]()
1. [What are getters/setters?]()
1. [How do you define a type alias in TypeScript? & Explain the purpose of type aliases in TypeScript.]()
1. [What is the difference between public, private, and protected access modifiers?]()
1. [Describe the difference between any and unknown types in Typescript. When would you use each?]()
1. [How do you handle null and undefined in TypeScript?]()
1. [Describe the difference between interface and type in TypeScript.]()

<br>


## 1️⃣ TypeScript-এর তিনটি main primitive data type কী?

TypeScript (এবং JavaScript)-এর তিনটি প্রধান primitive type হলো:

1. **string** → টেক্সট বা লেখা
2. **number** → সব ধরনের সংখ্যা (integer, float)
3. **boolean** → true / false

👉 এগুলো immutable (পরিবর্তন করা যায় না)

---

## 2️⃣ TypeScript-এ Interface কী?

**Interface** ব্যবহার করা হয় কোনো object-এর **structure বা shape define** করার জন্য।

👉 কোন property থাকবে
👉 কোন property-এর type কী হবে

**সহজভাবে:**

> Interface = object-এর নকশা (blueprint)

---

## 3️⃣ Type Assertion কী?

**Type assertion** দিয়ে আমরা TypeScript-কে বলি:

> “আমি জানি এই variable-এর actual type কী”

TypeScript নিজে বুঝতে না পারলে আমরা জোর দিয়ে type বলি।

👉 Runtime-এ কিছু change হয় না
👉 শুধু compiler-এর জন্য

---

## 4️⃣ TypeScript-এ কয়টি access modifier আছে?

TypeScript-এ **৩টি access modifier** আছে:

1. **public**
2. **private**
3. **protected**

---

## 5️⃣ Getters এবং Setters কী?

**Getter** → কোনো property-এর value **পড়ার জন্য**
**Setter** → কোনো property-এর value **set বা update করার জন্য**

👉 Encapsulation বজায় রাখতে সাহায্য করে
👉 Direct access নিয়ন্ত্রণ করা যায়

**সহজভাবে:**

> getter = read
> setter = write (control সহ)

---

## 6️⃣ Type Alias কীভাবে define করা হয়? এবং কেন ব্যবহার করা হয়?

### 🔹 Type Alias কী?

Type alias দিয়ে আমরা কোনো type-এর **নতুন নাম** দেই।

👉 object, union, primitive—সবকিছুর জন্য ব্যবহার করা যায়

### 🔹 কেন ব্যবহার করা হয়?

* Code readable হয়
* Reusable হয়
* Complex type সহজ হয়

**সহজভাবে:**

> Type alias = type-এর shortcut নাম

---

## 7️⃣ public, private, protected এর পার্থক্য কী?

* **public**
  👉 সব জায়গা থেকে access করা যায় (default)

* **protected**
  👉 class এবং তার child class থেকে access করা যায়

* **private**
  👉 শুধু class-এর ভিতরে access করা যায়

---

## 8️⃣ any ও unknown এর পার্থক্য কী? কখন কোনটা ব্যবহার করবেন?

### 🔹 any

* Type checking বন্ধ করে দেয়
* যেকোনো কিছু করা যায়
* Unsafe

### 🔹 unknown

* Safer version of any
* ব্যবহার করার আগে type check করতে হয়

👉 **Best practice:**

* Avoid `any`
* Prefer `unknown`

**সহজভাবে:**

> any = “যা খুশি”
> unknown = “আগে check করো”

---

## 9️⃣ TypeScript-এ null ও undefined কীভাবে handle করবেন?

TypeScript-এ সাধারণত **strictNullChecks** চালু থাকে।

👉 তখন:

* `null` ও `undefined` আলাদা type
* আগে check করতে হয়

ব্যবহার হয়:

* Optional chaining (`?.`)
* Nullish coalescing (`??`)

**সহজভাবে:**

> Error এড়াতে আগে null/undefined check করতে হবে

---

## 🔟 Interface এবং Type এর পার্থক্য কী?

### Interface

* Object-এর structure define করতে ভালো
* Extend করা যায়
* Class-এর সাথে ভালো কাজ করে

### Type

* Object + union + primitive সব define করা যায়
* Complex type-এর জন্য ভালো
* Intersection (`&`) ব্যবহার করা যায়

**সহজভাবে মনে রাখো:**

> Object shape → Interface
> Flexible & complex → Type

---
