<div align='center'>

# Object Oriented Programming (OOP)
</div>

## 📚 Table of Contents

- [1. Difference between Abstraction and Encapsulation (BrainStation)](#1-difference-between-abstraction-and-encapsulation--explain-with-examples-brainstation)

- [2. Difference between Overriding and Overloading (BS23)](#2-difference-between-overriding-and-overloading-bs23)

- [3. Final keyword in OOP (BrainStation | Prime Tech)](#3-final-keyword-in-oop--brainstation---prime-tech)

- [4. Difference between Interface and Abstract Class (BrainStation | CBG)](#4-difference-between-interface-and-abstract-class--brainstation--cbg)

- [5. Why is Interface important/main benifit? (Prime Tech)](#5-why-is-interface-importantmain-benifit--prime-tech)

- [6. Can we create an object of abstract class? (Prime Tech)](#6-can-we-create-an-object-of-abstract-class--prime-tech)


<br>

## 1. Difference between Abstraction and Encapsulation ? Explain with examples. (BrainStation)

নিচে **Abstraction** ও **Encapsulation** এর মধ্যে পার্থক্য সংক্ষেপে বাংলা ভাষায় উদাহরণসহ এবং একটি তুলনামূলক চার্ট আকারে দেওয়া হলো:

## 🔹 Abstraction (অ্যাবস্ট্রাকশন)
**অর্থ:** অপ্রয়োজনীয় তথ্য লুকিয়ে শুধুমাত্র দরকারি জিনিস দেখানো।
**🎯 লক্ষ্য:** ইউজারকে জটিলতা থেকে দূরে রাখা।

### 🧾 Example : 

```php
abstract class Shape {
    abstract public function area();
}

class Rectangle extends Shape {
    public function area() {
        return 10 * 20;
    }
}
```
👉 এখানে `Shape` ক্লাস ইউজারকে শুধু `area()` মেথড দেয়, ভিতরের হিসাব লুকানো থাকে।

### 🔹 Encapsulation (ইনক্যাপসুলেশন)
**অর্থ:** ডেটা ও ফাংশনকে একটি ইউনিটে বাঁধা এবং বাইরের থেকে ডেটা লুকানো।
**🎯 লক্ষ্য:** ডেটা সিকিউর করা ও নিয়ন্ত্রিত access দেওয়া।

### Example : 
```php
class BankAccount {
    private $balance = 0;

    public function deposit($amount) {
        if ($amount > 0) {
            $this->balance += $amount;
        }
    }

    public function getBalance() {
        return $this->balance;
    }
}
```
👉 এখানে balance প্রাইভেট, সরাসরি access করা যায় না। শুধু নির্ধারিত মেথড দিয়ে কাজ হয়।

### 📊 তুলনামূলক চার্ট: Abstraction vs Encapsulation

| বিষয়        | Abstraction (অ্যাবস্ট্রাকশন)                  | Encapsulation (ইনক্যাপসুলেশন)     |
| ----------- | --------------------------------------------- | --------------------------------- |
| উদ্দেশ্য    | জটিলতা লুকানো                                 | ডেটা সুরক্ষা ও নিয়ন্ত্রিত access  |
| কী লুকায়?   | বাস্তবায়নের জটিলতা (Implementation details)   | ডেটা (Data)                       |
| কীভাবে করে? |`abstract` class বা `interface` দিয়ে          | Access Modifier `private/protected` property দিয়ে |
| ফোকাস       | ইউজার কী দেখবে                                | ইউজার কীভাবে access করবে          |
| Example-1      | `area()` মেথডের ভিতরের লজিক না জানিয়ে ব্যবহার | `balance` ফিল্ড প্রাইভেট করে রাখা |
| Example-2     | A `RemoteControl` class with methods like `turnOn()`, `turnOff()`. User knows these actions exist, not how they work internally. | A `UserAccount` class with a private attribute `password` and methods `setPassword()`, `getPassword()`. Access to `password` is controlled. |


### 🧠 Summary
- **Abstraction** দেখায় কি হবে,
- **Encapsulation** নিয়ন্ত্রণ করে কিভাবে হবে এবং কে access পাবে।

<br>

## 2. Difference between Overriding and Overloading. (BS23)


### 🔹 **Overloading (ওভারলোডিং)**

একই নামে একাধিক মেথড/ফাংশন থাকা, কিন্তু আলাদা প্যারামিটার দিয়ে।

✅ **Occurs in:** Same class
✅ **Support in PHP:** সরাসরি না, কিন্তু `__call()` বা ম্যাজিক মেথড দিয়ে করা যায়।

**উদাহরণ (Other OOP Languages like Java):**

```java
class Math {
    int add(int a, int b) { return a + b; }
    double add(double a, double b) { return a + b; }
}
```

---

### 🔹 **Overriding (ওভাররাইডিং)**

প্যারেন্ট ক্লাসের মেথড চাইল্ড ক্লাসে নতুনভাবে সংজ্ঞায়িত করা।

✅ **Occurs in:** Parent-child (inheritance)
✅ **Support in PHP:** হ্যাঁ

**উদাহরণ (PHP):**

```php
class Animal {
    public function sound() {
        return "Some sound";
    }
}

class Dog extends Animal {
    public function sound() {
        return "Bark";
    }
}
```

---

## 📊 তুলনামূলক চার্ট: Overloading vs Overriding

| বিষয়             | Overloading (ওভারলোডিং)            | Overriding (ওভাররাইডিং)                      |
| ---------------- | ---------------------------------- | -------------------------------------------- |
| কাজ              | এক নামের একাধিক মেথড তৈরি          | প্যারেন্ট মেথডকে চাইল্ড ক্লাসে নতুনভাবে লেখা |
| ক্লাস সম্পর্ক    | একই ক্লাসে                         | ইনহেরিট করা ক্লাসে                           |
| প্যারামিটার      | আলাদা প্যারামিটার দরকার            | প্যারামিটার সাধারণত একই থাকে                 |
| PHP-তে সাপোর্ট   | সরাসরি না, ম্যাজিক মেথড দিয়ে সম্ভব | সম্পূর্ণ সাপোর্ট আছে                         |
| Example language | Java, C++, C# (native support)     | Java, PHP, C++ (inheritance-based)           
|Occurs|It occurs between two classes, Parent and Child class.|It occurs between two classes, Parent and Child class.
Parameter|Must be different|Must be same
Return Type|Can have different return types|Must be same

---

🧠 **সারাংশে:**

* **Overloading →** একই নাম, আলাদা প্যারামিটার
* **Overriding →** একই নাম ও প্যারামিটার, কিন্তু নতুন বাস্তবায়ন

<br>

## 3. 🔐`Final` keyword in OOP  `(BrainStation |  Prime Tech)`

`final` কীওয়ার্ড ব্যবহার করা হয় **কোনো ক্লাস বা মেথডকে override বা extend না করতে দেওয়ার জন্য**।

---

### 🔹 ১. **Final Class**

যদি কোনো ক্লাস `final` হয়, তাহলে সেই ক্লাসকে আর extend করা যাবে না।

```php
final class A {
    public function show() {
        echo "A class";
    }
}

// ❌ Error: Cannot extend final class A
class B extends A {}
```

---

### 🔹 ২. **Final Method**

যদি কোনো মেথড `final` হয়, তাহলে চাইল্ড ক্লাসে সেই মেথডকে override করা যাবে না।

```php
class A {
    final public function show() {
        echo "A class";
    }
}

class B extends A {
    // ❌ Error: Cannot override final method A::show()
    public function show() {
        echo "B class";
    }
}
```

---

### ✅ সারাংশ:

| বিষয়     | Final Class                   | Final Method                               |
| -------- | ----------------------------- | ------------------------------------------ |
| কী করে   | ক্লাস extend হওয়া বন্ধ করে    | মেথড override হওয়া বন্ধ করে                |
| উদ্দেশ্য | Structure লক করা, সিকিউর রাখা | নির্দিষ্ট মেথডের behavior অপরিবর্তনীয় রাখা |

<br>

## 4. Difference between Interface and Abstract Class ? `(BrainStation | CBG)`
নিচে **Interface** ও **Abstract Class** এর মধ্যে পার্থক্য সংক্ষেপে  দেওয়া হলো:

---

## 📘 সংজ্ঞা ও ব্যাখ্যা:

### 🔹 **Interface (ইন্টারফেস)**

* শুধুমাত্র মেথডের নাম থাকে, **কোনো implementation থাকে না**।
* সব মেথড **public** হয়।
* **multiple interface** implement করা যায়।

```php
interface Animal {
    public function makeSound();
}
```

---

### 🔹 **Abstract Class (অ্যাবস্ট্রাক্ট ক্লাস)**

* আংশিক বাস্তবায়ন থাকে: কিছু মেথড abstract, কিছু implemented থাকতে পারে।
* Property, constructor, এবং access modifier (private, protected) সাপোর্ট করে।

```php
abstract class Animal {
    abstract public function makeSound();

    public function sleep() {
        echo "Sleeping...";
    }
}
```

---

## 📊 তুলনামূলক চার্ট: Interface vs Abstract Class

| বিষয়                       | Interface (ইন্টারফেস)                     | Abstract Class (অ্যাবস্ট্রাক্ট ক্লাস)         |
| -------------------------- | ----------------------------------------- | --------------------------------------------- |
| বাস্তবায়ন (Implementation) | নেই, শুধু মেথডের নাম                      | থাকতে পারে (আংশিকভাবে)                        |
| প্রপার্টি                  | না (allowed না)                           | হ্যাঁ (allowed)                               |
| Access Modifier            | সব মেথড public                            | public, protected, private সব ব্যবহার করা যায় |
| Constructor                | না                                        | হ্যাঁ                                         |
| Multiple Implementation    | হ্যাঁ, একাধিক interface implement করা যায় | না, একটিই extend করা যায়                      |
Keywords| Used interface, implements| abstract class, extends,  abstract


---

🧠 **সারসংক্ষেপে:**

* **Interface →** ১০০% কাঠামো/নকশা (design only)
* **Abstract Class →** আংশিক কাঠামো + কিছু লজিক

## 5. Why is Interface important/main benifit ? `(Prime Tech)`


**Interface** OOP-এ গুরুত্বপূর্ণ কারণ এটি:

---

### 🔹 **মূল উপকারিতা:**

1. **🔄 Standard বা চুক্তি তৈরি করে**
   Interface বলে দেয়—যে ক্লাস এটা implement করবে, তাকে এই নির্দিষ্ট মেথডগুলো অবশ্যই রাখতে হবে।

2. **🤝 Loose Coupling (কম নির্ভরতাযুক্ত কোড)**
   আপনি interface এর উপর ভিত্তি করে কোড লিখলে ক্লাস বদলালেও পুরো সিস্টেম ভাঙে না।

3. **🔧 Multiple Inheritance সম্ভব**
   PHP তে একাধিক interface implement করা যায়, যেখানে একাধিক ক্লাস extend করা যায় না।

4. **📦 Dependency Injection সহজ হয়**
   Interface ব্যবহার করলে সার্ভিস, ক্লাস বা ফিচারগুলো সহজেই প্রতিস্থাপনযোগ্য (replaceable) হয়।
5. **Supports OCP (SOLID)** – Allows adding features without altering existing code.
6. **Scalability & Collaboration** – Facilitates teamwork and future expansion.
7. **Improved Testability** – Enables unit testing with mock implementations.

---

### 🧠 সংক্ষিপ্ত সারাংশ:

> **Interface** মূলত একটি কাঠামো বা নিয়ম নির্ধারণ করে, যা কোডকে আরো **flexible**, **পরিবর্তনযোগ্য** এবং **ভবিষ্যত উন্নয়নে সহায়ক** করে তোলে।


<br>

## 6. Can we create an object of abstract class ? `(Prime Tech)`


**না, পারি না।**

---

### 🔹 ব্যাখ্যা :

`abstract class` হচ্ছে **অসম্পূর্ণ (incomplete)** ক্লাস — যার কিছু মেথডের বাস্তবায়ন (implementation) নেই।
তাই সরাসরি তার অবজেক্ট তৈরি করলে বুঝতে পারবে না কী কাজ করবে।

```php
abstract class Animal {
    abstract public function sound();
}

// ❌ Error: Cannot instantiate abstract class
$animal = new Animal();
```

---

### ✅ তবে কী করা যায়?

আমরা **চাইল্ড ক্লাস** তৈরি করে, যেটা abstract ক্লাসকে **extend** করে,
তাতে সব মেথড implement করলে তার অবজেক্ট তৈরি করতে পারি।

```php
class Dog extends Animal {
    public function sound() {
        return "Bark";
    }
}

$dog = new Dog(); // ✅ ঠিক আছে
```

---

### 🧠 সংক্ষেপে:

> Abstract class → অবজেক্ট তৈরি **নয়**,
> কেবল **extend** করে ব্যবহার করতে হয়।

<br>

## 7. When to Use Parent Class vs. Traits ? `(CBG)`

## 🔷 1. **Use Parent Class when:**

| 📌                                                 | ব্যাখ্যা                                                                                           |
| -------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| 🧬 **Common Behavior বা Structure আছে**            | প্যারেন্ট ক্লাসে সাধারণ structure (property, constructor, method) থাকবে, যা সব চাইল্ডে থাকা দরকার। |
| 🧱 **Inheritance Relationship দরকার**              | যদি "is-a" সম্পর্ক থাকে (যেমন Dog is-an Animal), তখন প্যারেন্ট ক্লাস উপযুক্ত।                      |
| 🔁 **Method override করা লাগবে**                   | প্যারেন্ট ক্লাসের মেথড চাইল্ড ক্লাসে override করে পরিবর্তন করা যায়।                                |
| 👣 **Abstract বা বাস্তবায়িত মেথড মিশিয়ে দিতে চান** | কিছু method বাস্তবায়িত থাকবে, কিছু থাকবে abstract।                                                 |

**📌 উদাহরণ:**

```php
abstract class Animal {
    public function eat() {
        echo "Eating...";
    }

    abstract public function makeSound();
}

class Dog extends Animal {
    public function makeSound() {
        echo "Bark";
    }
}
```

---

## 🔶 2. **Use Traits when:**

| 📌                                                          | ব্যাখ্যা                                                                      |
| ----------------------------------------------------------- | ----------------------------------------------------------------------------- |
| ♻️ **Code Reuse দরকার, কিন্তু Inheritance না**              | Traits শুধু কোড শেয়ার করে, সম্পর্ক (relationship) তৈরি করে না।                |
| 🧩 **Multiple unrelated class এ একই logic দরকার**           | বিভিন্ন ক্লাসে একই মেথড ব্যবহার করতে হলে traits ভালো।                         |
| 🧱 **PHP supports only single inheritance**                 | একের বেশি প্যারেন্ট ক্লাস PHP-তে allowed না, কিন্তু একাধিক trait use করা যায়। |
| 🧰 **Utility/helper মেথড বা shared functionality দিতে চান** | যেমন: logging, file upload, reusable accessors ইত্যাদি।                       |

**📌 উদাহরণ:**

```php
trait Logger {
    public function log($msg) {
        echo "[LOG]: $msg";
    }
}

class Order {
    use Logger;
}

class User {
    use Logger;
}
```

---

## 📊 তুলনামূলক চার্ট:

| বিষয়          | Parent Class                    | Trait                                      |
| ------------- | ------------------------------- | ------------------------------------------ |
| Structure দেয় | হ্যাঁ (properties, constructor) | না                                         |
| Relationship  | Strong (is-a)                   | Weak (has-a / uses)                        |
| Multiple use  | একটাই extend করা যায়            | একাধিক trait use করা যায়                   |
| Code override | হ্যাঁ                           | সীমিত, method conflict হলে resolve করতে হয় |
| Use case      | Core behavior/model             | Shared reusable functionality              |

---

### 🧠 সংক্ষেপে সিদ্ধান্ত:

* 🔷 **Parent Class:** যখন আপনার ক্লাসগুলোর মধ্যে সত্যিকারের সম্পর্ক আছে।
* 🔶 **Traits:** যখন আপনি শুধু কিছু মেথড বা logic বিভিন্ন ক্লাসে reuse করতে চান, সম্পর্ক না থাকলেও।




