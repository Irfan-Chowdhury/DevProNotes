<div align='center'>

# PHP
</div>

## 📚 Table of Contents

1. [What is thread & Is PHP single or multi thread?](#what-is-thread--is-php-single-or-multi-thread) `[Branstaion23]`

1. [When and How do object of class initialize or not?](#when-and-how-do-object-of-class-initialize-or-not)

3. [What is SQL injection & how to protect in PHP ?](#what-is-sql-injection--how-to-protect-in-php)


4. [What is Vulnerability ?](#what-is-vulnerability) `[Business Automation]`

5. [What is Namespace ?](#what-is-namespace) `[Arraytics]`

6. [What is the difference between `echo` and `print` ?](#what-is-the-difference-between-echo-and-print)

7. [What are the differences among `include`, `require`, `include_once` and  `require_once` ?](#what-are-the-differences-among-include-require-include_once-and-require_once) `[CBG]`

8. [Difference between `Cookies` and `Session`](#difference-between-cookies--session) `[CBG]`


9. [What types of Error Handling?](#what-types-of-error-handling) `[CBG]`

10. [Difference between `isset()` and `empty()`](#difference-between-isset-and-empty) `[CBG]`

11. [What is Composer?](#what-is-composer) `[CBG]`

12. [How to handle the conflict of same method name in multiple `Traits` ?](#how-to-handle-the-conflict-of-same-method-name-in-multiple-traits) `[Brack IT]`




<br>

# # What is thread & Is PHP single or multi thread ?


### 🔍 **Thread কী?**

**Thread** হল একটি প্রোগ্রামের মধ্যে একক execution unit বা কাজের ধারা (flow)। একটি প্রোগ্রাম এক বা একাধিক থ্রেড ব্যবহার করতে পারে।

➡️ সহজভাবে বললে, **thread মানে এমন একটা লাইন যেটা কোড এক্সিকিউশন করে।**

A thread is like a single worker in a team. Each worker (thread) does its own job but
shares the same workspace (memory). For example, in a web browser, one thread might handle
loading a webpage, while another thread handles user interactions.

---

### ✅ **Single Thread vs Multi Thread**

| বিষয়        | Single Thread                | Multi Thread                   |
| ----------- | ---------------------------- | ------------------------------ |
| কাজের ধরণ   | একসাথে একটাই কাজ করে         | একসাথে একাধিক কাজ করতে পারে    |
| উদাহরণ      | PHP (by default), JavaScript | Java (with threading), C++, Go |
| Performance | কম কাজের জন্য ভালো           | অনেক কাজ একসাথে করলে efficient |

---

### ❓ **PHP কি Single-threaded নাকি Multi-threaded?**

🔸 **PHP মূলত Single-threaded.**

* PHP সাধারণত প্রতি HTTP অনুরোধে (request) একটি স্ক্রিপ্ট রান করে এবং সেটা সম্পূর্ণ শেষ হওয়ার পরেই আরেকটি অনুরোধ প্রসেস করে।
* অর্থাৎ, **একসাথে একাধিক কোড ব্লক বা থ্রেড এক্সিকিউট হয় না।**

🔸 তবে, PHP তে কিছু **multi-threading simulation বা parallel execution** করা যায় কিছু এক্সটেনশন দিয়ে, যেমন:

* **pthreads (old, only for CLI)**
* **parallel (modern replacement, PHP 7.2+ CLI)**
* **pcntl (for Unix systems only)**

❗ Web Server এ (যেমন Apache, Nginx) PHP সবসময় single-threaded হিসেবেই কাজ করে।

---

### 📌 উদাহরণ (Single-thread nature):

```php
echo "Start\n";
sleep(3); // ৩ সেকেন্ড ধরে প্রোগ্রাম থেমে থাকবে
echo "End\n";
```

➡️ এখানে `sleep()` এর সময় কোনো অন্য কাজ করা যাবে না, কারণ PHP একসাথে একাধিক থ্রেড চালাতে পারে না (default ভাবে)।

---

### ✅ সংক্ষেপে:

* **Thread** মানে execution line বা code চলার একটি ধারা।
* **PHP মূলত single-threaded**, অর্থাৎ এক সময়ে একটাই কাজ করতে পারে।
* যদি parallel processing দরকার হয়, তাহলে বিশেষ এক্সটেনশন বা অন্য টেকনোলজি ব্যবহার করতে হয়।

---

<br>

# # When and How do object of class initialize or not ?


## 🔹 **Object কখন initialize হয় ?**

➡️ যখন আপনি `new` কীওয়ার্ড ব্যবহার করে কোন ক্লাসের একটি instance তৈরি করেন, তখন সেই ক্লাসের একটি **object initialize** হয়।

```php
class Car {
    public function __construct() {
        echo "Car object তৈরি হয়েছে!";
    }
}

$myCar = new Car(); // Output: Car object তৈরি হয়েছে!
```

* এখানে `new Car()` বলার সাথে সাথেই:

  * মেমোরিতে নতুন অবজেক্ট তৈরি হয়
  * `__construct()` নামে যদি কোন constructor method থাকে, সেটি **অটোমেটিক্যালি কল হয়**
  * অবজেক্টটি `$myCar` ভেরিয়েবলে সংরক্ষিত হয়

---

### 🔹 **Object কিভাবে initialize হয় (Step by Step)?**

```php
class Person {
    public $name;

    public function __construct($name) {
        $this->name = $name;
        echo "Person: $name তৈরি হয়েছে\n";
    }
}

$p1 = new Person("Irfan");
```

🔸 ব্যাখ্যা:

1. `new Person("Irfan")` কল করা হয়েছে
2. PHP মেমোরিতে `Person` ক্লাসের একটি অবজেক্ট তৈরি করে
3. Constructor `__construct()` কল হয়, যেখানে `$name` প্যারামিটার হিসাবে "Irfan" যায়
4. অবজেক্ট `$p1` তে সংরক্ষিত হয়

---

## ❌ **Object কখন initialize হয় না?**

### 1. **`new` না দিলে**

```php
class Bike {
    public function __construct() {
        echo "Bike created";
    }
}

// এখানে কোন object তৈরি হয়নি
```

➡️ শুধুমাত্র class define করলেই object তৈরি হয় না।

---

### 2. **Constructor এ parameter দরকার, কিন্তু না দিলে**

```php
class User {
    public function __construct($id) {
        echo "User ID: $id";
    }
}

$user = new User(); // ❌ Fatal Error: missing argument
```

➡️ `__construct()` এ যদি প্যারামিটার লাগে, কিন্তু আপনি না দেন, তাহলে object তৈরি হবে না, বরং error দিবে।

---

### 3. **Class name শুধু ভেরিয়েবলে রাখলে**

```php
$className = "Car"; // এটা শুধু string, কোন object না
```

➡️ এখানে object initialize হয়নি, কারণ `new` ব্যবহার হয়নি।

---

## 🔁 **সারাংশ (সংক্ষেপে)**

| ঘটনা/অবস্থা                     | Object তৈরি হয়? | ব্যাখ্যা                   |
| ------------------------------- | --------------- | -------------------------- |
| `new ClassName()`               | ✅ হ্যাঁ         | মূলভাবে object তৈরি হয়     |
| Constructor-এ parameter না দিলে | ❌ না            | Error দেয়                  |
| শুধু class define করলে          | ❌ না            | Object তৈরি হয় না          |
| Static method থেকে create করলে  | ✅ হ্যাঁ         | Factory pattern ব্যবহার হয় |

---


## 🧠 **উপসংহার:**

* **new** ব্যবহার করলেই object তৈরি হয়
* constructor থাকলে সেটি অটো কল হয়
* parameter ভুল দিলে object তৈরি হয় না
* factory/static method দিয়েও object তৈরি সম্ভব

---

<br>

# # What is SQL injection & how to protect in PHP ?


## 💣 **SQL Injection কী?**

**SQL Injection** হল একটি **হ্যাকার অ্যাটাক টেকনিক**, যেখানে ইউজার ইনপুটের মাধ্যমে malicious (খারাপ) SQL কোড পাঠিয়ে ডেটাবেজে অবাঞ্ছিত কাজ করানো হয় — যেমন:

* ডেটা চুরি
* ডেটা মুছে ফেলা
* অ্যাডমিন একসেস পাওয়া
* এমনকি পুরো ডেটাবেজ নষ্ট করে ফেলা

---

### 🔥 উদাহরণ (ভুল পদ্ধতি):

```php
$username = $_GET['username'];
$password = $_GET['password'];

$query = "SELECT * FROM users WHERE username = '$username' AND password = '$password'";
$result = mysqli_query($conn, $query);
```

**ইনপুট দিলে**:

```
username = ' OR 1=1 --
password = কিছু দরকার নাই
```

➡️ তখন query হবে:

```sql
SELECT * FROM users WHERE username = '' OR 1=1 -- ' AND password = ''
```

📌 এখানে `OR 1=1` সব রেকর্ড রিটার্ন করবে, `--` বাকি অংশকে comment করে দেয়। এতে attacker লগিন করতে পারবে।

---

## ✅ PHP-তে SQL Injection থেকে বাঁচার উপায়:

### 🔐 1. **Prepared Statements (PDO বা MySQLi ব্যবহার করে)**

#### ✅ PDO (PHP Data Object) ব্যবহার:

```php
$pdo = new PDO("mysql:host=localhost;dbname=test", "root", "");

$stmt = $pdo->prepare("SELECT * FROM users WHERE username = :username AND password = :password");

$stmt->execute([
    'username' => $_POST['username'],
    'password' => $_POST['password']
]);

$user = $stmt->fetch();
```

➡️ এখানে `:username` এবং `:password` placeholders, যা user input কে **bind** করে, সরাসরি query-তে বসায় না। এতে injection হয় না।

---

#### ✅ MySQLi Prepared Statement:

```php
$conn = new mysqli("localhost", "root", "", "test");

$stmt = $conn->prepare("SELECT * FROM users WHERE username = ? AND password = ?");
$stmt->bind_param("ss", $username, $password);

$username = $_POST['username'];
$password = $_POST['password'];

$stmt->execute();
$result = $stmt->get_result();
```

---

### 🧱 2. **User Input Validate ও Filter করুন**

* Email field হলে `filter_var($email, FILTER_VALIDATE_EMAIL)`
* Integer হলে `(int)$id` বা `ctype_digit($id)`
* শুধু A-Z হলে `preg_match('/^[a-zA-Z]+$/', $input)`

---

### 🚫 3. **Never use raw SQL with user input**

এভাবে কোড লেখা উচিত নয়:

```php
"DELETE FROM users WHERE id = $_GET[id]"
```

এখানে `$_GET['id']` সরাসরি বসালে হ্যাকার যেকোনো ID delete করতে পারবে।

---

### 🔐 4. **Web Application Firewall (WAF) বা Security Tools ব্যবহার করুন**

যেমন:

* ModSecurity
* Suhosin (PHP Security Patch)

---

### ✅ সংক্ষেপে: SQL Injection থেকে বাঁচার উপায়

| উপায়                           | ব্যাখ্যা                                     |
| ------------------------------ | -------------------------------------------- |
| ✅ Prepared Statements          | PDO বা MySQLi দিয়ে input আলাদা করে bind করুন |
| ✅ Input Validation & Filtering | ইউজার ইনপুট যাচাই করুন                       |
| ❌ Raw Query এ ইনপুট বসানো      | সরাসরি input বসালে injection হতে পারে        |
| ✅ Error message hide করুন      | ভেতরের SQL error ইউজারকে দেখাবেন না          |
| ✅ WAF/Security tools           | অতিরিক্ত নিরাপত্তা নিশ্চিত করে               |

---

## 🔐 উপসংহার:

**"Prepared Statement"** হলো সবচেয়ে নিরাপদ পদ্ধতি SQL Injection থেকে বাঁচার জন্য।
PHP দিয়ে ডেটাবেজে কাজ করার সময় সবসময় PDO বা MySQLi ব্যবহার করুন।

---

<br>

# # What is Vulnerability ?

**Vulnerability (দুর্বলতা)** হলো সফটওয়্যার, কনফিগারেশন বা সার্ভার পরিবেশে থাকা এমন কোনো ভুল, ফাঁকফোকর বা দুর্বলতা, যেটা হ্যাকার বা আক্রমণকারী ব্যবহার করে সিস্টেমে অনুপ্রবেশ, ডেটা চুরি বা ক্ষতি করতে পারে।

---

### 🧠 উদাহরণ দিয়ে সহজভাবে বোঝা যাক:

> 1. যদি আপনার ওয়েবসাইটে পাসওয়ার্ড ফর্মে ঠিকমতো validation না থাকে, তাহলে হ্যাকার সেই ফর্মে SQL injection দিয়ে ডেটাবেসে ঢুকে যেতে পারে। এটাকে বলে **SQL Injection Vulnerability**


   

> 2. যদি কোনো সফটওয়্যারে পুরানো লাইব্রেরি ব্যবহার করা হয় যেটায় নিরাপত্তাজনিত ত্রুটি আছে, সেটাও Vulnerability।


---

## 🧨 PHP তে সাধারণ Vulnerability-এর ধরনসমূহ:

### 1. ✅ **SQL Injection (SQLi)**

**বর্ণনা:** ইউজার ইনপুটকে সরাসরি SQL কুয়েরিতে যুক্ত করার ফলে হ্যাকার ডেটাবেসে ইচ্ছামত প্রশ্ন করতে পারে।
**দুর্বল কোড (উদাহরণ):**

```php
$id = $_GET['id'];
$query = "SELECT * FROM users WHERE id = $id";
```

**সমাধান:** Prepared statements বা PDO ব্যবহার করুন।

---

### 2. ✅ **Cross-Site Scripting (XSS)**

**বর্ণনা:** ম্যালিশাস স্ক্রিপ্ট ইনজেক্ট করে ব্রাউজারে চালানো হয়, যা ইউজারের কুকি বা তথ্য চুরি করতে পারে।
**দুর্বল কোড (উদাহরণ):**

```php
echo $_POST['comment'];  // ইনপুট Escape না করলে ঝুঁকি
```

**সমাধান:** `htmlspecialchars()` ব্যবহার করে ইনপুট Escape করুন।

---

### 3. ✅ **File Inclusion Vulnerability**

**বর্ণনা:** ইউজার থেকে আসা ইনপুট ব্যবহার করে যদি ফাইল `include` করা হয়, তাহলে হ্যাকার অন্য কোড চালাতে পারে।
**উদাহরণ:**

```php
include($_GET['page']);
```

**সমাধান:** নির্দিষ্ট অনুমোদিত ফাইল লিস্ট থেকে পছন্দ করতে দিন।

---

### 4. ✅ **Cross-Site Request Forgery (CSRF)**

**বর্ণনা:** ইউজার লগইন থাকা অবস্থায় তাকে না জানিয়ে কিছু কাজ করিয়ে ফেলা (যেমন: পাসওয়ার্ড পরিবর্তন)।

**সমাধান:** ফর্মে CSRF টোকেন ব্যবহার করুন (Laravel এ ডিফল্ট থাকে)।

---

### 5. ✅ **Remote Code Execution (RCE)**

**বর্ণনা:** হ্যাকার সার্ভারে কোড চালাতে পারে যদি ইনপুট সঠিকভাবে যাচাই না করা হয়।
**উদাহরণ:**

```php
eval($_GET['code']); // বিপজ্জনক
```

**সমাধান:** `eval()` এবং অনুরূপ ফাংশন এড়িয়ে চলুন।

---

## 🛡️ কিভাবে PHP Vulnerability প্রতিরোধ করবেন?

✅ নিরাপদ কোডিং প্র্যাকটিস অনুসরণ করুন <br>
✅ ইনপুট ভ্যালিডেশন ও সেনিটাইজেশন করুন <br>
✅ Prepared Statements ব্যবহার করুন (SQL এর জন্য) <br>
✅ `htmlspecialchars()` বা Blade escaping ব্যবহার করুন (XSS থেকে রক্ষা পেতে) <br>
✅ CSRF টোকেন নিশ্চিত করুন <br>
✅ অপ্রয়োজনীয় ফাংশন বা এক্সটেনশন বন্ধ রাখুন

---

## 🔍 উপসংহার:

PHP অ্যাপে vulnerability থাকলে তা দিয়ে হ্যাকার আপনার ডেটা চুরি, ওয়েবসাইট হ্যাক বা সার্ভার নষ্ট করে দিতে পারে। তাই সচেতনভাবে কোড লেখা, ইনপুট যাচাই করা এবং আপডেটেড ফ্রেমওয়ার্ক ব্যবহার করা নিরাপত্তার জন্য অত্যন্ত জরুরি।

---

<br>

# # What is Namespace ?


### 📘 সংজ্ঞা:

**Namespace** হলো PHP-র একটি ফিচার যা একই নামের ক্লাস, ফাংশন, বা কনস্ট্যান্টকে বিভিন্ন জায়গায় ব্যবহার করতে দেয় — সংঘর্ষ (conflict) ছাড়াই।

> এক কথায়, Namespace হচ্ছে কোড সংগঠনের একটি উপায়, যা বড় প্রজেক্টে ক্লাস ও ফাংশনের নাম ম্যানেজ করতে সাহায্য করে।

---

### 🎯 উদাহরণ দিয়ে সহজভাবে বোঝা যাক:

ধরুন, আপনার প্রজেক্টে দুইটি `User` নামের ক্লাস আছে –
একটি `Admin` প্যানেলের জন্য, অন্যটি `Frontend` ইউজারের জন্য।

```php
// Admin এর User class
namespace App\Admin;

class User {
    public function role() {
        return 'Admin';
    }
}
```

```php
// Frontend এর User class
namespace App\Frontend;

class User {
    public function role() {
        return 'Customer';
    }
}
```

এখন আপনি চাইলে দুইটা ক্লাসই ব্যবহার করতে পারেন:

```php
use App\Admin\User as AdminUser;
use App\Frontend\User as FrontendUser;

$admin = new AdminUser();
echo $admin->role(); // Admin

$frontend = new FrontendUser();
echo $frontend->role(); // Customer
```

---

### ✅ কেন Namespace ব্যবহার করবেন?

* **নাম সংঘর্ষ (Name conflict)** এড়াতে
* **বড় প্রজেক্টে ক্লাস ফাইল গুলো সংগঠিত রাখতে**
* **PSR-4 Autoloading** সহজ করতে (Composer ব্যবহার করলে)

---

### 🔧 Laravel এ Namespace এর ব্যবহার:

Laravel-এ প্রতিটি ক্লাসের শুরুতেই সাধারণত একটি `namespace` থাকে।

```php
// app/Http/Controllers/HomeController.php
namespace App\Http\Controllers;

class HomeController extends Controller {
    public function index() {
        return view('home');
    }
}
```

আর আপনি Route এ ব্যবহার করেন:

```php
use App\Http\Controllers\HomeController;

Route::get('/', [HomeController::class, 'index']);
```

---

### 📌 উপসংহার:

> Namespace হলো আপনার প্রজেক্টের **address system** — যেভাবে রাস্তার ঠিকানা বাড়িগুলো আলাদা করে, namespace তেমনি কোডের নামগুলো আলাদা করে।

---

<br>

# # What is the difference between `echo` and `print` ?


## 🆚 `echo` বনাম `print` 

| বিষয়                          | `echo`                                       | `print`                               |
| ----------------------------- | -------------------------------------------- | ------------------------------------- |
| ✅ **প্রধান কাজ**              | ডাটা/টেক্সট আউটপুট দেখায়                     | ডাটা/টেক্সট আউটপুট দেখায়              |
| 🧠 **টাইপ**                   | Language construct (ভাষার গঠনী)              | Language construct                    |
| 🔁 **রিটার্ন ভ্যালু**         | কিছু রিটার্ন করে না                          | `1` রিটার্ন করে (এটা একটি এক্সপ্রেশন) |
| 💬 **একাধিক আর্গুমেন্ট**      | একাধিক ভ্যালু নিতে পারে (কমা দিয়ে আলাদা করে) | কেবলমাত্র একটি ভ্যালু নিতে পারে       |
| ⚡ **গতি (speed/performance)** | সামান্য দ্রুত                                | তুলনামূলক ধীর                         |
| 🧱 **সিনট্যাক্স উদাহরণ**      | `echo "Hello", " World!";` ✅                 | `print("Hello World!");` ✅            |

---

### 🎯 উদাহরণ:

#### 🟢 `echo` এর ব্যবহার:

```php
echo "Hello", " World!";  // একাধিক স্ট্রিং প্রিন্ট করা যায়
```

#### 🟡 `print` এর ব্যবহার:

```php
print "Hello World!";  // কেবল একটাই স্ট্রিং নেয়
```

#### 🔴 ভুল:

```php
print "Hello", " World!"; // ❌ Error: একাধিক আর্গুমেন্ট নেয় না
```

---

### 🔍 কোনটা ব্যবহার করবেন?

* ✅ যদি শুধু আউটপুট দেখাতে চান → `echo` ব্যবহার করাই ভালো (কারণ এটা দ্রুততর এবং ফ্লেক্সিবল)
* ✅ যদি আউটপুট করার পাশাপাশি return value দরকার হয় → `print` ব্যবহার করা যায় (যেমন: কন্ডিশনের ভিতরে)

---

### 📌 উপসংহার:

> `echo` বেশি দ্রুত, একাধিক মান নিতে পারে এবং সাধারণত বেশি ব্যবহৃত হয়। আর `print` একটি ভ্যালু রিটার্ন করে এবং একটু ধীর হলেও নির্দিষ্ট প্রয়োজনে কার্যকর।

---

<br>

# # What are the differences among `include`, `require`, `include_once` and  `require_once` ?

PHP-তে `include`, `require`, `include_once`, এবং `require_once` ফাংশনগুলো ব্যবহার করা হয় এক ফাইল থেকে অন্য ফাইল যুক্ত করার জন্য (code reusability)। তবে এগুলোর মধ্যে কিছু পার্থক্য আছে, যেটা বুঝে ব্যবহার করা জরুরি।

---

## 📘 ১. `include`

🔹 কোনো ফাইল **যোগ করতে** ব্যবহৃত হয়। <br>
🔹 যদি ফাইল না পাওয়া যায়, তাহলে **warning** দেখায় কিন্তু **script চলা বন্ধ করে না**।

```php
include 'header.php';
echo "Page content";
```

✅ ফাইল থাকলে `header.php` যোগ হবে, <br>
❌ না থাকলে warning দেখাবে কিন্তু `Page content` ঠিকই চলবে।

---

## 📘 ২. `require`

🔹 `include` এর মতোই কাজ করে — ফাইল যুক্ত করে। <br>
🔹 কিন্তু যদি ফাইল না পাওয়া যায়, তাহলে **fatal error** হয় এবং **script execution বন্ধ হয়ে যায়**।

```php
require 'header.php';
echo "Page content";
```

❌ যদি `header.php` না থাকে, তাহলে `Page content` আর দেখা যাবে না।

---

## 📘 ৩. `include_once`

🔹 একবারই ফাইল যুক্ত করে, এমনকি একাধিকবার লিখলেও। <br>
🔹 যদি আগেই include হয়ে থাকে, তাহলে দ্বিতীয়বার আর যুক্ত করে না।

```php
include_once 'functions.php';
include_once 'functions.php'; // দ্বিতীয়বার আর লোড হবে না
```

✅ ডুপ্লিকেট inclusion বন্ধ করে।

---

## 📘 ৪. `require_once`

🔹 `require` + `once` = ফাইল একবারই রিকোয়ার করবে, <br>
🔹 না থাকলে fatal error, <br>
🔹 এবং থাকলেও বারবার যুক্ত করবে না।

```php
require_once 'config.php';
require_once 'config.php'; // দ্বিতীয়বার আর লোড হবে না
```

---

## 🔍 তুলনা টেবিল:

| ফাংশন          | ফাইল না থাকলে কী হয়?        | ডুপ্লিকেট লোড বন্ধ করে? |
| -------------- | --------------------------- | ----------------------- |
| `include`      | Warning, চলা চালু থাকে      | না ❌                    |
| `require`      | Fatal Error, স্ক্রিপ্ট থামে | না ❌                    |
| `include_once` | Warning, চলা চালু থাকে      | হ্যাঁ ✅                 |
| `require_once` | Fatal Error, স্ক্রিপ্ট থামে | হ্যাঁ ✅                 |

---

## ✅ কখন কোনটা ব্যবহার করবেন?

* 🔹 ফাইল **অপশনাল** হলে ➤ `include` বা `include_once`
* 🔹 ফাইল **অবশ্যই থাকা লাগবে** ➤ `require` বা `require_once`
* 🔹 বড় প্রজেক্টে `once` ভার্সনগুলোই ভালো, কারণ এটি **ডুপ্লিকেট লোড** প্রতিরোধ করে
---

<br>

# # Difference between `Cookies` & `Session`


## 🍪 Cookies কী?

Cookies হলো ছোট ছোট ডেটা ফাইল যেগুলো **ব্রাউজারে (client side)** সংরক্ষিত হয়।

### ✅ Cookies-এর বৈশিষ্ট্য:

* ইউজারের ব্রাউজারে সংরক্ষিত হয়।
* সাধারণত key-value আকারে থাকে।
* সার্ভার থেকে পাঠানো হয়, ইউজারের ব্রাউজারে সেট হয়।
* ইউজার পরের বার ওয়েবসাইটে গেলে সেই cookie আবার সার্ভারে পাঠায়।

### 📦 উদাহরণ:

যদি তুমি কোনো ওয়েবসাইটে language preference বাংলা সেট করো, তবে সেটি cookie-তে রাখা যেতে পারে। ফলে পরবর্তীতে ব্রাউজারে সেই তথ্য থেকে আবার বাংলা দেখাবে।

---

## 🧠 Session কী?

Session হলো **সার্ভার সাইডে** ইউজার-সম্পর্কিত তথ্য সংরক্ষণের একটি উপায়।

### ✅ Session-এর বৈশিষ্ট্য:

* সার্ভারে সংরক্ষিত হয়।
* ইউজারকে একটি unique session ID দেওয়া হয় (সেটি cookie বা URL এ পাঠানো হয়)।
* sensitive বা বড় তথ্য রাখার জন্য ভালো।
* একাধিক পেইজে ইউজার লগইন থাকলে সেই তথ্য session-এ থাকে।

### 📦 উদাহরণ:

তুমি লগইন করলে — তোমার ইউজারের তথ্য (ID, Name ইত্যাদি) সার্ভারের session-এ রাখা হয়। তুমি যত পেইজে যাও না কেন, তুমি logged-in থাকো কারণ session তোমাকে চিনে রাখে।

---

## 🔄 Cookies vs Session (তফাৎ):

| বিষয়               | Cookie                    | Session                                       |
| ------------------ | ------------------------- | --------------------------------------------- |
| সংরক্ষণ কোথায়?     | ইউজারের ব্রাউজারে         | সার্ভারে                                      |
| সিকিউরিটি          | তুলনামূলক কম              | বেশি                                          |
| ডেটার আকার         | ছোট                       | তুলনামূলক বড়                                  |
| ব্যবহারের উদ্দেশ্য | user preference, tracking | authentication, temporary data                |
| মেয়াদ              | expiration date সহ        | browser বন্ধ হলে শেষ বা সময়সীমা নির্ধারণযোগ্য |

---

## 🧪 PHP-তে উদাহরণ:

**Cookie সেট করা:**

```php
setcookie("user", "irfan", time() + 3600); // ১ ঘণ্টার জন্য
```

**Session শুরু ও ব্যবহার:**

```php
session_start();
$_SESSION['user'] = "irfan";
```

---

## ✅ উপসংহার:

* **Cookie**: ব্রাউজারে ছোট তথ্য সংরক্ষণ করে, যেমন ইউজারের পছন্দ।
* **Session**: সার্ভারে তথ্য রাখে, সাধারণত authentication বা sensitive data এর জন্য।

---

<br>

# # What types of Error Handling ?

PHP-তে **Error Handling** বলতে বুঝায় এমন একটি ব্যবস্থা যার মাধ্যমে প্রোগ্রাম চলাকালে যেকোনো ধরনের ভুল (Error) ধরা, রিপোর্ট করা এবং প্রয়োজনমতো সেগুলো সামাল দেওয়া যায়।

---

## 🔍 PHP-তে Error Handling-এর প্রধান ধরনগুলো:

### 1. **Syntax Error (Parse Error)**

* কোডে ভুল syntax থাকলে হয়।
* যেমন: সেমিকোলন না দেওয়া, বন্ধনী ভুল ইত্যাদি।

🧪 উদাহরণ:

```php
echo "Hello World"  // সেমিকোলন নেই
```

> ⚠️ PHP এই কোড রান করবে না এবং সরাসরি error দেখাবে।

---

### 2. **Runtime Error**

* কোড ঠিকঠাক লেখা থাকলেও, execution-এর সময় সমস্যা হয়।
* যেমন: undefined variable, file না পাওয়া, division by zero ইত্যাদি।

🧪 উদাহরণ:

```php
echo $x; // $x defined নয়
```

---

### 3. **Logical Error**

* কোড চালু হয়, কিন্তু ফলাফল ভুল আসে।
* PHP কোনো error message দেখায় না, কিন্তু প্রোগ্রাম ঠিকমতো কাজ করে না।

🧪 উদাহরণ:

```php
$total = 10 + 5 * 2; // চাইলে আগে যোগফল পেতে, কিন্তু এখানে গুন আগে হয়েছে
```

---

### 4. **Fatal Error**

* খুব গুরুতর error, execution থেমে যায়।
* যেমন: undefined function call, class না থাকা ইত্যাদি।

🧪 উদাহরণ:

```php
nonExistentFunction(); // এই function নেই
```

---

### 5. **Warning**

* ছোটখাটো সমস্যা, execution থামে না, কিন্তু warning দেখায়।

🧪 উদাহরণ:

```php
include("file_that_does_not_exist.php"); // ফাইল নেই
```

---

### 6. **Notice**

* হালকা সতর্কতা, কোড চালু থাকে, কিন্তু কিছু issue থাকে।
* যেমন: undefined variable ব্যবহার করা।

---

## ✅ Modern PHP Error Handling Tools:

### 1. **Try-Catch Block**

```php
try {
    // সমস্যা হতে পারে এমন কোড
    throw new Exception("Something went wrong!");
} catch (Exception $e) {
    echo "Error: " . $e->getMessage();
}
```

### 2. **Custom Error Handler**

```php
function customError($errno, $errstr) {
    echo "Custom Error: [$errno] $errstr";
}

set_error_handler("customError");
echo($test); // test defined না
```

### 3. **Error Reporting Level Set**

```php
error_reporting(E_ALL);
ini_set('display_errors', 1);
```

---

## 🧾 Summary Table:

| Error Type    | Description                         | Impact             |
| ------------- | ----------------------------------- | ------------------ |
| Syntax Error  | ভুল কোড structure                   | Execution বন্ধ     |
| Runtime Error | Execution সময় সমস্যা                | কখনো বন্ধ, কখনো না |
| Logical Error | ভুল ফলাফল                           | Execution চলে      |
| Fatal Error   | মারাত্মক সমস্যা, function/class নাই | Execution বন্ধ     |
| Warning       | ফাইল না পাওয়া ইত্যাদি               | Warning দেখায়      |
| Notice        | ছোটখাটো সমস্যা (e.g. undefined var) | চলতে থাকে          |

---

<br>

# # Difference between `isset()` and `empty()`

PHP-তে `isset()` এবং `empty()` — এই দুটি ফাংশন প্রায়ই ব্যবহার হয় **ভ্যারিয়েবল চেক** করার জন্য, কিন্তু এগুলোর কাজ আলাদা।

---

## 🔍 মূল পার্থক্য:

| বিষয়          | `isset()`                                                     | `empty()`                                   |
| ------------- | ------------------------------------------------------------- | ------------------------------------------- |
| কাজ           | চেক করে ভ্যারিয়েবল **সেট আছে কিনা** (i.e. exists এবং null নয়) | চেক করে ভ্যারিয়েবলটি **খালি বা falsy** কিনা |
| রিটার্ন করে   | `true` যদি ভ্যারিয়েবল **সেট** থাকে এবং `null` না হয়           | `true` যদি ভ্যারিয়েবল **empty/falsy** হয়    |
| null চেক      | `null` হলে `false` রিটার্ন করে                                | `null` হলে `true` রিটার্ন করে               |
| undefined চেক | কাজ করে না (Notice error দিতে পারে না)                        | কাজ করে, Error ছাড়াই `true` দেয়             |

---

## 🧪 উদাহরণসহ ব্যাখ্যা:

### 🔸 `isset()` উদাহরণ:

```php
$a = null;

if (isset($a)) {
    echo "Set"; 
} else {
    echo "Not set"; // Output হবে: Not set
}
```

`$a` ভ্যারিয়েবল সেট থাকলেও তার মান `null`, তাই `isset()` → `false` রিটার্ন করে।

---

### 🔸 `empty()` উদাহরণ:

```php
$b = 0;

if (empty($b)) {
    echo "Empty"; // Output হবে: Empty
} else {
    echo "Not empty";
}
```

`$b` এর মান `0`, যেটা **falsy**, তাই `empty()` → `true` রিটার্ন করে।


## ✅ কখন কোনটা ব্যবহার করব?

* 🔍 `isset()` → যদি তুমি চাও ভ্যারিয়েবল **সেট** আছে কিনা এবং `null` নয়, সেটা জানতে।
* 🕳️ `empty()` → যদি তুমি চাও ভ্যারিয়েবলটি **"খালি বা false টাইপ" মান** (যেমন `0`, `""`, `false`, `null`, `[]`) রাখে কিনা, সেটা জানতে।


## 📦 Falsy values যেগুলো `empty()` → `true` দেয়:

* `""` (empty string)
* `0` (integer)
* `"0"` (string)
* `null`
* `false`
* `[]` (empty array)
* unset variable


## 📌 শেষ কথা:

* ✅ `isset()` → চেক করে **ভ্যারিয়েবল সেট আছে কিনা এবং null নয় কিনা**।
* ✅ `empty()` → চেক করে **ভ্যারিয়েবল "খালি বা falsy" কিনা**।

---

<br>

# # What is Composer ?


**Composer** হলো PHP-র জন্য একটি **dependency management tool**, যা তোমার প্রোজেক্টে দরকারি লাইব্রেরি/প্যাকেজগুলো install, update, এবং manage করার কাজ করে।

---

## 🔍 সহজ কথায়:

> Composer এমন একটি টুল, যেটা দিয়ে তুমি তোমার প্রোজেক্টে দরকারি **external library বা package** গুলো **install, update, autoload** করতে পারো খুব সহজে।

---

## 🧾 উদাহরণ:

তুমি যদি Laravel প্রোজেক্ট তৈরি করো, তাহলে Laravel framework-টা Composer দিয়েই install হয়:

```bash
composer create-project laravel/laravel my-app
```

---

## 🧱 Composer কীভাবে কাজ করে?

1. **composer.json** ফাইলে declare করো কোন প্যাকেজগুলো লাগবে।
2. Composer সেইসব প্যাকেজ গুলোকে ডাউনলোড করে `vendor/` ফোল্ডারে রাখে।
3. তারপর `vendor/autoload.php` ফাইলে সবকিছু **autoload** করে।

---

## ⚙️ Example: `composer.json`

```json
{
  "require": {
    "guzzlehttp/guzzle": "^7.0"
  }
}
```

এই কোডে বলা আছে যে আমাদের `guzzlehttp/guzzle` প্যাকেজ লাগবে।

---

## 🔧 Common Composer Commands:

| Command                           | কাজ                                     |
| --------------------------------- | --------------------------------------- |
| `composer init`                   | নতুন composer.json তৈরি করে             |
| `composer install`                | composer.lock দেখে প্যাকেজ ইন্সটল করে   |
| `composer update`                 | composer.json দেখে সর্বশেষ প্যাকেজ আনবে |
| `composer require vendor/package` | নতুন প্যাকেজ যোগ করে                    |
| `composer dump-autoload`          | autoloader regenerate করে               |

---

## ✅ Composer কেন দরকার?

* Dependency manage করতে
* অটোমেটিক autoload তৈরি করতে
* ভার্সন কন্ট্রোল সহজ করতে
* প্যাকেজ দ্রুত আপডেট করতে
* লাইব্রেরি গুলোর conflict এড়াতে

---

## 📦 Composer দিয়ে কি কি install করা যায়?

* Laravel
* PHPUnit (Testing)
* Guzzle (HTTP client)
* Spatie packages
* Filament, Pest ইত্যাদি

---

## 📌 উপসংহার:

> Composer ছাড়া modern PHP development একপ্রকার অসম্ভব। এটা তোমার প্রোজেক্টের structure সুন্দর করে, সময় বাঁচায় এবং dependency conflict রোধ করে।

---

<br>

# # How to handle the conflict of same method name in multiple `Traits` ? 

When **multiple traits** in PHP contain **methods with the same name**, PHP will throw a **fatal error** unless you handle the **conflict explicitly**.

---

## 🔥 সমস্যা কবে হয়?

```php
trait A {
    public function sayHello() {
        echo "Hello from A";
    }
}

trait B {
    public function sayHello() {
        echo "Hello from B";
    }
}

class MyClass {
    use A, B; // ❌ Fatal error: sayHello() conflict
}
```

উপরের ক্ষেত্রে `sayHello()` method দুই trait-এ থাকায় PHP জানে না কোনটা ব্যবহার করবে — তাই **error** দেয়।

---

## ✅ সমাধান: `insteadof` এবং `as`

PHP-তে `insteadof` ব্যবহার করে বলো কোন trait-এর method ব্যবহার করবে, আর `as` দিয়ে alias তৈরি করতে পারো।

### ✔️ উদাহরণ:

```php
trait A {
    public function sayHello() {
        echo "Hello from A\n";
    }
}

trait B {
    public function sayHello() {
        echo "Hello from B\n";
    }
}

class MyClass {
    use A, B {
        B::sayHello insteadof A;     // B's version will be used
        A::sayHello as sayHelloFromA; // A's version will be aliased
    }
}

$obj = new MyClass();
$obj->sayHello();        // Output: Hello from B
$obj->sayHelloFromA();   // Output: Hello from A
```

---

## ✅ সারাংশ:

* একাধিক Trait ব্যবহারে method name conflict হলে PHP error দেয়।
* `insteadof` দিয়ে নির্ধারণ করো কোনটা override করবে।
* `as` দিয়ে অন্যটার নতুন নাম দিয়ে access করো।
* এই পদ্ধতিতে তুমি দুইটাকেই একসাথে ব্যবহার করতে পারো।

---



