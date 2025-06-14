<div align='center'>

# Application Programming Interface (API) | Interview Preparation
</div>

## 📚 Table of Contents

### ✅ Basic Level

1. [What is a RESTful API?](#1-what-is-a-restful-api)
2. [REST আর্কিটেকচারের মূল নীতিমালা (Principles of REST Architecture)](#2-rest-আর্কিটেকচারের-মূল-নীতিমালা-principles-of-rest-architecture)
3. [What is the difference between PUT and PATCH?](#3-what-is-the-difference-between-put-and-patch)
4. [What is the purpose of HTTP methods like GET, POST, PUT, DELETE?](#4-what-is-the-purpose-of-http-methods-like-get-post-put-delete)
5. [What status codes are commonly used in REST APIs?](#5-what-status-codes-are-commonly-used-in-rest-apis)
6. [What is the difference between URI and URL?](#6-what-is-the-difference-between-uri-and-url)
7. [Is REST stateful or stateless? Why?](#7-is-rest-stateful-or-stateless-why)
8. [What is the use of the `OPTIONS` method in REST APIs?](#8-what-is-the-use-of-the-options-method-in-rest-apis)

### ✅ Intermediate Level

9. [How do you handle authentication in RESTful APIs?](#9-how-do-you-handle-authentication-in-restful-apis)
10. [How do you implement versioning in REST APIs?](#10-how-do-you-implement-versioning-in-rest-apis)
11. [What are idempotent methods? Which HTTP methods are idempotent?](#11-what-are-idempotent-methods-which-http-methods-are-idempotent)
12. [How do you handle pagination in REST APIs?](#12-how-do-you-handle-pagination-in-rest-apis)
13. [How do you secure REST APIs? (Rate limiting, input validation, HTTPS, etc.)](#13-how-do-you-secure-rest-apis-rate-limiting-input-validation-https-etc)
14. [What is HATEOAS and is it required in REST?](#14-what-is-hateoas-and-is-it-required-in-rest)
15. [What are some best practices for designing RESTful endpoints?](#15-what-are-some-best-practices-for-designing-restful-endpoints-eg-resource-based-urls-plural-nouns-nested-routes)
16. [How do you differentiate between 404 Not Found and 204 No Content?](#16-how-do-you-differentiate-between-404-not-found-and-204-no-content)

### ✅ Advanced Level

17. [How would you design an API for file upload/download?](#17-how-would-you-design-an-api-for-file-uploaddownload)  
18. [How do you handle long-running operations in a REST API?](#18-how-do-you-handle-long-running-operations-in-a-rest-api)  
19. [What are webhooks and how do they differ from REST APIs?](#19-what-are-webhooks-and-how-do-they-differ-from-rest-apis)  
20. [What is the N+1 query problem in REST APIs and how can you prevent it?](#20-what-is-the-n1-query-problem-in-rest-apis-and-how-can-you-prevent-it)  
21. [How would you design a REST API rate-limiting system?](#21-how-would-you-design-a-rest-api-rate-limiting-system)  
22. [How do you test REST APIs (unit/integration)? (e.g., tools like Postman, PHPUnit, PEST, or automated tests)](#22-how-do-you-test-rest-apis-unitintegration-eg-tools-like-postman-phpunit-pest-or-automated-tests)  
23. [How would you structure a RESTful API in a microservice architecture?](#23-how-would-you-structure-a-restful-api-in-a-microservice-architecture)  


<br>
<br>


# 1. What is a RESTful API ?

**RESTful API** অর্থ হলো এমন একটি API (Application Programming Interface) যা **REST (Representational State Transfer)** আর্কিটেকচারের নিয়ম অনুসরণ করে কাজ করে।

---

### 🔍 RESTful API কী?

**RESTful API** হলো এমন একটি ওয়েব সার্ভিস যা HTTP প্রোটোকল ব্যবহার করে ক্লায়েন্ট এবং সার্ভারের মধ্যে ডেটা আদান-প্রদান করে। এটি **stateless**, অর্থাৎ প্রতিটি অনুরোধ (request) স্বতন্ত্র, এবং সার্ভার পূর্বের কোনো তথ্য মনে রাখে না।

---

### 🧩 উদাহরণ দিয়ে ব্যাখ্যা:

ধরুন, আপনার একটি ই-কমার্স ওয়েবসাইট আছে এবং আপনি প্রোডাক্টের তথ্য দেখতে চান। তখন আপনি নিচের মতো একটি URL ব্যবহার করতে পারেন:

```
GET /api/products
```

এখানে:

* `GET` হলো HTTP method (তথ্য নেওয়ার জন্য),
* `/api/products` হলো endpoint (product লিস্ট পাওয়ার জন্য)।

---

### 🔑 RESTful API-এর মূল বৈশিষ্ট্য:

1. **Stateless** – প্রতিটি অনুরোধ আলাদা এবং সার্ভার আগে কী হয়েছে তা মনে রাখে না।
2. **Resource-Based** – API গুলো সাধারণত resource (যেমন: user, product) ভিত্তিক হয়।
3. **HTTP Methods ব্যবহার করে** – যেমন:

   * `GET` – ডেটা রিড করতে
   * `POST` – নতুন ডেটা তৈরি করতে
   * `PUT` – সম্পূর্ণ আপডেট করতে
   * `PATCH` – আংশিক আপডেট করতে
   * `DELETE` – ডেটা ডিলিট করতে
4. **JSON/ XML format** – ডেটা আদান-প্রদানের জন্য সাধারণত JSON ব্যবহার হয়।

---

### 🎯 সংক্ষেপে:

> **RESTful API** হলো এমন একটি ওয়েব API যেটি HTTP method এবং নির্দিষ্ট নিয়ম মেনে ক্লায়েন্ট-সার্ভারের মধ্যে তথ্য আদান-প্রদান করে। এটি দ্রুত, নির্ভরযোগ্য এবং সহজবোধ্য একটি পদ্ধতি ওয়েব সার্ভিস তৈরি করার জন্য।

<br>


# 2. REST আর্কিটেকচারের মূল নীতিমালা (Principles of REST Architecture)




1. **Stateless (অবস্থা-নিরপেক্ষ)**
   – প্রতিটি request সম্পূর্ণ তথ্য থাকে, সার্ভার কিছু মনে রাখে না।

2. **Client-Server (ক্লায়েন্ট-সার্ভার বিভাজন)**
   – ক্লায়েন্ট UI নিয়ে কাজ করে, সার্ভার ডেটা ও লজিক নিয়ন্ত্রণ করে।

3. **Uniform Interface (একইধরনের ইন্টারফেস)**
   – সব API এক নিয়মে কাজ করে (যেমন: `/api/users`, `/api/products` ইত্যাদি)।

4. **Cacheable (ক্যাশযোগ্য)**
   – ডেটা ক্যাশ করা যায় পারফরম্যান্স বাড়াতে।

5. **Layered System (স্তরভিত্তিক কাঠামো)**
   – API বিভিন্ন লেয়ারে কাজ করতে পারে যেমন: গেটওয়ে, অথেন্টিকেশন সার্ভার ইত্যাদি।

6. **Code on Demand (ঐচ্ছিক)**
   – প্রয়োজনে সার্ভার ক্লায়েন্টকে স্ক্রিপ্ট (যেমন JavaScript) পাঠাতে পারে।

---

| Principles                  | Meaning                |
| ------------------------- | --------------------------- |
| Stateless                 | অবস্থা-নিরপেক্ষ             |
| Client-Server             | ক্লায়েন্ট-সার্ভার ভিত্তিক  |
| Uniform Interface         | অভিন্ন ইন্টারফেস            |
| Cacheable                 | ক্যাশযোগ্য                  |
| Layered System            | স্তরবিন্যাস কাঠামো          |
| Code on Demand (Optional) | অনুরোধে কোড পাঠানো (ঐচ্ছিক) |


> এই নীতিগুলো অনুসরণ করলেই একটা API হয়ে ওঠে RESTful API.


<br>

# 3. What is the difference between PUT and PATCH ?

নিচে `PUT` ও `PATCH` এর সংক্ষিপ্ত বাংলা ব্যাখ্যা দেওয়া হলো:

---

### 🔁 **PUT** – সম্পূর্ণ আপডেট

* সম্পূর্ণ রিসোর্স **update** করে।
* সব ফিল্ড পাঠাতে হয়, না পাঠালে আগের ডেটা মুছে যেতে পারে।
* যেমন: নতুন করে পুরো তথ্য দিতে হয়।

---

### 🔧 **PATCH** – আংশিক আপডেট

* শুধু যেই ফিল্ড পরিবর্তন করতে চান, সেটাই পাঠান।
* আগের বাকি ডেটা ঠিক থাকে।
* যেমন: শুধু নাম আপডেট করতে চাইলে শুধু `name` পাঠালেই হবে।

---

### 📌 পার্থক্য সংক্ষেপে:

| বিষয়                | PUT                 | PATCH             |
| ------------------- | ------------------- | ----------------- |
| আপডেট টাইপ          | সম্পূর্ণ            | আংশিক             |
| সব ফিল্ড দরকার?     | হ্যাঁ               | না                |
| আগের ডেটা মুছে যায়? | হ্যাঁ, যদি না পাঠান | না                |
| উদাহরণ              | পুরো প্রোফাইল আপডেট | শুধু নাম পরিবর্তন |

---

✅ মনে রাখার কৌশল:
**PUT = পুরোটাই আপডেট করো**,
**PATCH = প্যাঁচ দিয়ে শুধু দরকারি অংশ বদলাও**।

<br>

# 4. What is the purpose of HTTP methods like GET, POST, PUT, DELETE?

নিচে HTTP methods গুলোর উদ্দেশ্য সংক্ষেপে বাংলায় ব্যাখ্যা করা হলো:

---

### ✅ HTTP Methods এর উদ্দেশ্য:

| Method     | কাজ (Purpose)                        | উদাহরণ                               |
| ---------- | ------------------------------------ | ------------------------------------ |
| **GET**    | ডেটা **তুলে আনা** (Read)             | `/api/users` → সব ইউজার দেখানো       |
| **POST**   | নতুন ডেটা **তৈরি করা** (Create)      | `/api/users` → নতুন ইউজার তৈরি       |
| **PUT**    | সম্পূর্ণ **আপডেট করা** (Full Update) | `/api/users/1` → ইউজার পুরো পরিবর্তন |
| **PATCH**  | আংশিক **আপডেট করা** (Partial Update) | `/api/users/1` → শুধু নাম বদলানো     |
| **DELETE** | ডেটা **মুছে ফেলা** (Delete)          | `/api/users/1` → ইউজার ডিলিট         |

---

### 🎯 মনে রাখার কৌশল:

* **GET = পাওয়া**
* **POST = তৈরি করা**
* **PUT = পুরোটা বদলানো**
* **PATCH = কিছুটা বদলানো**
* **DELETE = মুছে ফেলা**

এই ৫টি মেথড RESTful API ডিজাইনে সবচেয়ে বেশি ব্যবহৃত হয়।

<br>

# 5. What status codes are commonly used in REST APIs?

নিচে REST API-তে সবচেয়ে বেশি ব্যবহৃত কিছু **HTTP status code** এর বাংলা ব্যাখ্যা সংক্ষেপে দেওয়া হলো:

---

### ✅ Commonly Used HTTP Status Codes (in Bangla)

| Status Code                   | অর্থ / ব্যাখ্যা                            | কখন ব্যবহার হয়                          |
| ----------------------------- | ------------------------------------------ | --------------------------------------- |
| **200 OK**                    | সফলভাবে অনুরোধ সম্পন্ন হয়েছে               | ডেটা রিড (GET) বা সফল অপারেশন           |
| **201 Created**               | নতুন রিসোর্স সফলভাবে তৈরি হয়েছে            | POST অনুরোধের পর                        |
| **204 No Content**            | সফল কিন্তু কোনো কনটেন্ট নেই                | সফলভাবে ডিলিট হয়েছে, কিন্তু রেসপন্স নেই |
| **400 Bad Request**           | অনুরোধ ভুল ছিল (invalid data)              | ভ্যালিডেশন বা ইনপুটে সমস্যা             |
| **401 Unauthorized**          | অথেন্টিকেশন দরকার                          | লগইন না করে request করা হয়েছে           |
| **403 Forbidden**             | অনুমতি নেই (permission denied)             | লগইন আছে, কিন্তু কাজটি করার অনুমতি নেই  |
| **404 Not Found**             | রিসোর্স পাওয়া যায়নি                        | ভুল URL বা ID                           |
| **422 Unprocessable Entity**  | ইনপুট ঠিক আছে, কিন্তু প্রসেস করা যাচ্ছে না | Laravel validation error                |
| **500 Internal Server Error** | সার্ভার-সাইড সমস্যা                        | কোড বা সার্ভারে ভুল                     |

---

### 🎯 মনে রাখার সহজ উপায়:

* `200` → সব ঠিকঠাক
* `201` → নতুন কিছু তৈরি
* `400` → তুমি ভুল পাঠিয়েছো
* `401`/`403` → অনুমতি নাই
* `404` → পাই নাই
* `500` → আমি (সার্ভার) গড়বড় করে ফেলেছি

---

<br>

# 6. What is the difference between URI and URL?
### ✅ URI ও URL এর পার্থক্য

| বিষয়      | URI                                                  | URL                                |
| --------- | ---------------------------------------------------- | ---------------------------------- |
| পূর্ণ রূপ | Uniform Resource Identifier                          | Uniform Resource Locator           |
| কাজ       | রিসোর্স শনাক্ত করে                                   | রিসোর্সের অবস্থান (location) দেখায় |
| কী থাকে   | নাম বা অবস্থান যেকোনোটি                              | কেবল ঠিকানা (location)             |
| উদাহরণ    | `urn:isbn:1234567890`<br>`https://example.com/about` | `https://example.com/about`        |

---

### 🎯 সহজভাবে:

* **URI**: রিসোর্স চিনে (নাম বা ঠিকানা দিয়ে)
* **URL**: রিসোর্স **কোথায় আছে** তা বলে (ওয়েব ঠিকানা)

📌 সব URL-ই URI, কিন্তু সব URI URL না।

<br>

# 7. Is REST stateful or stateless? Why? 

**REST হল Stateless** (অবস্থা-নিরপেক্ষ) আর্কিটেকচার।

---

### Why:

* প্রতিটি HTTP অনুরোধে (request) সার্ভার **নিজের কোন আগের তথ্য/Session মনে রাখে না**।
* যদি ক্লায়েন্ট টোকেন না দেয়, সার্ভার ইউজার চেনতে পারবে না।
* অনুরোধের সঙ্গে সব প্রয়োজনীয় তথ্য থাকতে হয়, যেন সার্ভার একেকটি অনুরোধকে স্বাধীন ভাবে প্রসেস করতে পারে।
* এর ফলে সার্ভার সহজে স্কেল করা যায়, কারণ সার্ভারের কাছে ক্লায়েন্টের অবস্থা (state) সংরক্ষণ করার ঝামেলা নেই।
* Stateless হওয়ার কারণে, যখনই কোনো অনুরোধ আসে, সেটাকে আলাদা ও স্বতন্ত্রভাবে হ্যান্ডেল করা হয়।

---

### সংক্ষেপে:

**REST API-তে ক্লায়েন্ট এবং সার্ভারের মাঝে কোন অবস্থা (state) শেয়ার করা হয় না।** প্রতিটি অনুরোধ নিজেই সম্পূর্ণ।

---

### উদাহরণ:

যদি আপনি কোনো REST API-তে কোনো ইউজারের তথ্য দেখতে চান, তাহলে আপনার অনুরোধের সঙ্গে ইউজার আইডি বা টোকেন দিতে হবে, সার্ভার আগের কোন সেশন বা তথ্য মনে রাখবে না।


<br>

# 8. What is the use of the `OPTIONS` method in REST APIs?

**OPTIONS** হল একটি `HTTP মেথড` যা সার্ভারের কাছে জানতে চায়:
**"এই URL এ কোন কোন HTTP মেথডগুলো সমর্থিত?"**

অর্থাৎ, ক্লায়েন্ট জানতে চায় যে, এই রিসোর্সে কী কী ধরণের অনুরোধ (GET, POST, PUT, DELETE, ইত্যাদি) করা যাবে।

---

### কেন দরকার?

* **CORS (Cross-Origin Resource Sharing)** এর সময় ব্রাউজার যখন অন্য ডোমেইন থেকে API কল করে, তখন প্রথমে OPTIONS রিকোয়েস্ট পাঠায় (preflight request)।
* এটি সার্ভারের কাছ থেকে অনুমতি চায়, যেন পরবর্তীতে মূল অনুরোধ (যেমন POST বা PUT) করা যায়।
* OPTIONS রিকোয়েস্টের জবাবে সার্ভার জানায় কোন মেথড এবং হেডার গ্রহণযোগ্য।

---

### সহজ উদাহরণ:

* ক্লায়েন্ট `/api/users` রিসোর্সে OPTIONS রিকোয়েস্ট পাঠাবে।
* সার্ভার রেসপন্স দেবে:

  ```
  Allow: GET, POST, PUT, DELETE
  Access-Control-Allow-Origin: *
  Access-Control-Allow-Methods: GET, POST, PUT, DELETE
  ```

এতে ক্লায়েন্ট জানতে পারবে ওই URL এ কোন কোন মেথড ব্যবহার করতে পারবে।

---

### সংক্ষেপে:

| OPTIONS মেথড | REST API-তে কী করে?                                      |
| ------------ | -------------------------------------------------------- |
| কাজ          | রিসোর্সে কোন HTTP মেথডগুলো অনুমোদিত তা জানায়             |
| ব্যবহৃত হয়   | মূলত CORS-এর preflight রিকোয়েস্টে এবং মেথড চেক করার জন্য |

---

> **OPTIONS** মেথড বলে দেয়, "এই URL-এ কী কী কাজ করা যাবে?"
এটি ক্লায়েন্ট ও সার্ভারের মধ্যে নিরাপদ যোগাযোগ নিশ্চিত করে।

<br>

# 9. How do you handle authentication in RESTful APIs ? 


### Authentication কি?

Authentication হলো ব্যবহারকারীর পরিচয় যাচাই করার প্রক্রিয়া, যাতে নিশ্চিত হওয়া যায় যে, API-তে যারা এক্সেস করছে তারা অনুমোদিত।

---

### RESTful API তে Authentication এর জনপ্রিয় পদ্ধতি:

#### ১. Token-Based Authentication (টোকেন ভিত্তিক)

* ইউজার প্রথমে লগইন করে ইউজারনেম ও পাসওয়ার্ড পাঠায়।
* সফল লগইনের পর সার্ভার একটি **টোকেন** (যেমন JWT, Laravel Sanctum Token) তৈরি করে দেয়।
* পরবর্তীতে ক্লায়েন্ট প্রতিটি অনুরোধের সাথে ওই টোকেন পাঠায়।
* সার্ভার টোকেন ভেরিফাই করে অনুরোধ প্রক্রিয়া করে।
* সার্ভার কোনো সেশন মনে রাখে না (stateless)।

**Laravel এ:** Laravel Sanctum বা Passport ব্যবহার করে সহজেই Token Authentication করা যায়।

---

#### ২. Basic Authentication (বেসিক অথেন্টিকেশন)

* ইউজারনেম ও পাসওয়ার্ড প্রতি অনুরোধের হেডারে base64 এ এনকোড করে পাঠানো হয়।
* সাধারণত SSL দিয়ে প্রোটেক্টেড API তে ব্যবহার করা হয় কারণ পাসওয়ার্ড হেডারে পাঠানো হয়।

---

#### ৩. OAuth2 Authentication

* বড় বড় সিস্টেমে ব্যবহৃত হয় যেখানে তৃতীয় পক্ষের (third-party) মাধ্যমে অথেন্টিকেশন দিতে হয়।
* Laravel Passport এই OAuth2 প্রটোকল সাপোর্ট করে।

---

### সংক্ষেপে Authentication Flow:

1. ইউজার লগইন করে (POST /login)।
2. সার্ভার টোকেন দিয়ে ফিরে আসে।
3. ক্লায়েন্ট প্রতিটি অনুরোধে `Authorization: Bearer <token>` হেডার পাঠায়।
4. সার্ভার টোকেন যাচাই করে ডেটা রিটার্ন করে।
5. টোকেন না থাকলে বা ভুল হলে 401 Unauthorized রেসপন্স যায়।

---

### উদাহরণ (Laravel Sanctum):

```php
// Login API - Token Generate
public function login(Request $request) {
    $user = User::where('email', $request->email)->first();

    if (!$user || !Hash::check($request->password, $user->password)) {
        return response()->json(['message' => 'Invalid credentials'], 401);
    }

    $token = $user->createToken('api-token')->plainTextToken;

    return response()->json(['token' => $token]);
}

// Protected route
Route::middleware('auth:sanctum')->get('/profile', function (Request $request) {
    return $request->user();
});
```

---

### সারাংশ:

> RESTful API তে Authentication সাধারণত **টোকেন ভিত্তিক হয়**, যেখানে প্রতিটি অনুরোধে টোকেন পাঠিয়ে সার্ভার অথেন্টিকেশন করে। এতে API stateless থাকে এবং নিরাপদ হয়।

<br>

# 10. How do you implement versioning in REST APIs ?

API Versioning মানে হলো API এর বিভিন্ন সংস্করণ (version) আলাদা করে রাখা যাতে ভবিষ্যতে নতুন ফিচার যোগ করার সময় পুরানো API ব্যবহারকারীরা ক্ষতিগ্রস্ত না হন।

---

### কেন দরকার?

* API ক্রমাগত পরিবর্তিত হয়।
* নতুন ফিচার যোগ করলে পুরানো ক্লায়েন্টের কাজ বন্ধ না হয়।
* বিভিন্ন ভার্সন একসাথে মেইনটেইন করা যায়।

---

### Versioning ইমপ্লিমেন্টের সাধারণ ৩টি পদ্ধতি:

---

#### ১. URL Path Versioning (সবচেয়ে জনপ্রিয়)

* API URL এর মধ্যে ভার্সন যুক্ত করা হয়।
* উদাহরণ:

  ```
  /api/v1/products
  /api/v2/products
  ```
* সহজে বুঝতে পারা যায় এবং ব্রাউজার বা কনসিউমারদের কাছে স্পষ্ট হয়।

---

#### ২. Request Header Versioning

* ভার্সন তথ্য HTTP হেডারে পাঠানো হয়।
* উদাহরণ:

  ```
  Accept: application/vnd.example.v1+json
  ```
* API URL একই থাকে, হেডারের মাধ্যমে ভার্সন বুঝানো হয়।
* কিছু ক্ষেত্রে ব্যবহার হয়, কিন্তু বেশি জটিল।

---

#### ৩. Query Parameter Versioning

* URL এর query param দিয়ে ভার্সন পাঠানো হয়।
* উদাহরণ:

  ```
  /api/products?version=1
  ```
* সহজ কিন্তু URL একটু জটিল হতে পারে।

---

### Laravel এ URL Path Versioning উদাহরণ:

```php
// routes/api.php

Route::prefix('v1')->group(function () {
    Route::get('/products', [ProductController::class, 'indexV1']);
});

Route::prefix('v2')->group(function () {
    Route::get('/products', [ProductController::class, 'indexV2']);
});
```

* এখানে `/api/v1/products` এবং `/api/v2/products` আলাদা হ্যান্ডলার ব্যবহার করছে।
* আপনি চাইলে পুরানো ভার্সনের API রাখতে পারেন এবং নতুন ভার্সনে পরিবর্তন যোগ করতে পারেন।

---

### সারাংশ:

> * API Versioning করে আপনি একসাথে একাধিক সংস্করণ মেইনটেইন করতে পারেন।
> * সবচেয়ে সহজ ও সাধারণ পদ্ধতি হলো URL এর মধ্যে ভার্সন নম্বর রাখা, যেমন `/api/v1/...`।
> * Versioning API-এর ভবিষ্যৎ রক্ষণাবেক্ষণে খুবই গুরুত্বপূর্ণ।

<br>

# 11. What are idempotent methods? Which HTTP methods are idempotent ?


### ✅ Idempotent Method কী ?

**Idempotent** মানে হলো, **একই রিকোয়েস্ট যতবারই পাঠানো হোক না কেন, সার্ভারের রিসোর্সে একই ফলাফল থাকবে — কোনো অতিরিক্ত পরিবর্তন হবে না।**

অর্থাৎ, আপনি ১ বার করেন বা ১০ বার করেন, রিসোর্সের অবস্থা এক থাকবেই।

---

### 🧠 উদাহরণ:

```http
PUT /api/products/5 {"stock": 100}
```

* আপনি এই PUT রিকোয়েস্ট ১০ বার পাঠালেও, `stock` হবে ১০০-ই। মান আবার আবার সেট হলেও অতিরিক্ত কোনো পরিবর্তন হবে না।
* তাই এটি idempotent।

---

### ✅ কোন HTTP Methods গুলো Idempotent?

| HTTP Method | Idempotent? | ব্যাখ্যা                                                                           |
| ----------- | ----------- | ---------------------------------------------------------------------------------- |
| **GET**     | ✅ হ্যাঁ     | শুধু ডেটা রিটার্ন করে, কিছু পরিবর্তন করে না।                                       |
| **PUT**     | ✅ হ্যাঁ     | নির্দিষ্ট রিসোর্সকে নির্দিষ্ট মানে পরিবর্তন করে। একই অনুরোধ বারবার দিলে একই ফলাফল। |
| **DELETE**  | ✅ হ্যাঁ     | একবার রিসোর্স মুছে ফেললে, বারবার মুছতে গেলেও অবস্থার পরিবর্তন হবে না।              |
| **HEAD**    | ✅ হ্যাঁ     | কেবল হেডার ফেরত দেয়, কিছু পরিবর্তন করে না।                                         |
| **OPTIONS** | ✅ হ্যাঁ     | সার্ভারের অনুমোদিত মেথড জানায়, রিসোর্সে প্রভাব ফেলে না।                            |
| **POST**    | ❌ না        | POST দিয়ে প্রতিবার নতুন রিসোর্স তৈরি হয়, তাই এটি idempotent না।                    |

---

### 📝 সারাংশ:

> ✅ **Idempotent methods** হলো এমন HTTP মেথড যেগুলো একাধিকবার চালালেও সার্ভারের অবস্থা একই থাকে।
>
> ✔️ `GET`, `PUT`, `DELETE`, `HEAD`, `OPTIONS` → Idempotent
>
> ❌ `POST` → Not Idempotent

---

<br>

# 12. How do you handle pagination in REST APIs?

**Pagination** হলো একটি বড় ডেটা সেটকে ছোট ছোট অংশে ভাগ করা — যেন ক্লায়েন্ট একসাথে সব ডেটা না নিয়ে পেজ বাই পেজ (page by page) ডেটা দেখতে পারে।

---

### ✅ কেন Pagination দরকার?

* পারফরম্যান্স বাড়ায় (কম ডেটা একবারে লোড হয়)
* ক্লায়েন্ট ও সার্ভারে লোড কমে
* UI-তে ইউজার ফ্রেন্ডলি ভিউ পাওয়া যায়

---

### 🔧 Pagination কিভাবে করা হয় REST API তে?

সাধারণভাবে query parameters ব্যবহার করা হয়:

```
GET /api/products?page=2&per_page=10
```

এখানে:

* `page=2` → কোন পেজে যাবে
* `per_page=10` → প্রতি পেজে কয়টি আইটেম

---

### 🔍 উদাহরণ (Laravel):

```php
// Controller method
public function index(Request $request)
{
    return Product::paginate(10); // প্রতি পেজে ১০টি প্রোডাক্ট
}
```

**Response JSON:**

```json
{
  "current_page": 1,
  "data": [
    { "id": 1, "name": "Product A" },
    ...
  ],
  "last_page": 5,
  "per_page": 10,
  "total": 50
}
```

---

### 🛠️ Laravel এর কিছু Pagination Method:

* `paginate(n)` → সাধারণ pagination
* `simplePaginate(n)` → শুধুমাত্র previous/next
* `cursorPaginate(n)` → বড় ডেটার জন্য efficient pagination

---

### 📝 সারাংশ :

> REST API-তে Pagination মানে হচ্ছে ডেটা ছোট ছোট পেজে ভাগ করা, যেমন `/api/products?page=1&per_page=10`। Laravel-এ আপনি `paginate()` ফাংশন ব্যবহার করে সহজেই এটা করতে পারেন।

<br>

# 13. How do you secure REST APIs? (Rate limiting, input validation, HTTPS, etc.)



REST API নিরাপদ রাখতে হলে নিচের বিষয়গুলো অনুসরণ করতে হয় — যাতে হ্যাকার, স্প্যাম বা অসতর্ক ব্যবহারে ডেটা ক্ষতিগ্রস্ত না হয়।

---

### ✅ ১. **Authentication & Authorization**

* **Authentication**: কে API access করছে যাচাই করা (যেমন: Token, JWT, OAuth)
* **Authorization**: কে কী করতে পারবে সেটা নির্ধারণ করা
* 🔐 Laravel এ Sanctum বা Passport দিয়ে সহজেই করা যায়।

---

### ✅ ২. **HTTPS ব্যবহার করুন**

* HTTP নয়, **HTTPS** ব্যবহার করুন — এতে ডেটা এনক্রিপ্টেড থাকে।
* লগইন, পেমেন্ট, প্রাইভেট API — সবকিছুই HTTPS ছাড়া করা উচিত নয়।

---

### ✅ ৩. **Rate Limiting**

* এক ইউজার এক নির্দিষ্ট সময়ের মধ্যে কতবার API access করতে পারবে, সেটা নিয়ন্ত্রণ করা।
* উদাহরণ: প্রতি মিনিটে সর্বোচ্চ 60 অনুরোধ।
* Laravel এ `throttle` middleware ব্যবহার করে সহজেই করা যায়।

```php
Route::middleware('throttle:60,1')->group(function () {
    Route::get('/user', function () {
        // 60 request per minute allowed
    });
});
```

---

### ✅ ৪. **Input Validation & Sanitization**

* ব্যবহারকারীর ইনপুট যাচাই করা (যেমন: email, password, etc.)
* SQL injection, XSS থেকে বাঁচাতে অবশ্যই ইনপুট ভ্যালিডেট করতে হবে।
* Laravel এ FormRequest বা `$request->validate()` দিয়ে করা হয়।

```php
$request->validate([
    'email' => 'required|email',
    'password' => 'required|min:8',
]);
```

---

### ✅ ৫. **CORS (Cross-Origin Resource Sharing) কনফিগার করুন**

* নির্ধারণ করুন কোন origin থেকে API কল করা যাবে।
* Laravel এ `fruitcake/laravel-cors` middleware বা Laravel 7+ এর built-in support ব্যবহার করা হয়।

---

### ✅ ৬. **Hide Sensitive Data**

* কখনই Token, Password, Database Error API Response এ দেখাবেন না।
* Debug mode সবসময় production এ বন্ধ রাখতে হবে।

```env
APP_DEBUG=false
```

---

### ✅ ৭. **Logging & Monitoring**

* সন্দেহজনক request লগ করে রাখতে হবে।
* IP-based logging, 401/403 রিকোয়েস্ট মনিটরিং করতে হবে।

---

### ✅ ৮. **Use API Keys (if applicable)**

* Third-party ইউজারের জন্য API key দিয়ে নির্ধারণ করা যায় কে কোন API access করতে পারবে।

---

### ✅ ৯. **Use CSRF Protection (for web-based APIs)**

* যদি আপনার API ওয়েব ফর্মের মাধ্যমে access করে, তাহলে CSRF টোকেন ব্যবহার করা উচিত।

---

### 🔐 সারাংশ:

> REST API সুরক্ষিত রাখতে হলে আপনাকে Authentication, HTTPS, Rate Limiting, Input Validation, এবং CORS-এর মতো সিকিউরিটি প্র্যাকটিস ফলো করতে হবে।

---

<br>

# 14. What is HATEOAS and is it required in REST?


### ✅ HATEOAS কী? 

**HATEOAS** এর পূর্ণরূপ হলো:
**Hypermedia As The Engine Of Application State**

এটি REST আর্কিটেকচারের একটি **উন্নত লেভেলের নীতি**, যেখানে API response-এর মধ্যে **পরবর্তী করণীয় কাজের লিংক বা নির্দেশনাও** দেওয়া থাকে।

---

### 🧠 সহজভাবে:

যখন আপনি API থেকে ডেটা নেন, তখন সেটার সাথে সাথে **"আপনি এখন কী করতে পারেন"** সেই লিংকও পাবেন।

---

### 🧾 উদাহরণ:

একটি প্রোডাক্ট ডেটা যদি এমনভাবে পাঠানো হয়:

```json
{
  "id": 5,
  "name": "Shirt",
  "price": 500,
  "links": [
    { "rel": "self", "href": "/api/products/5" },
    { "rel": "update", "href": "/api/products/5" },
    { "rel": "delete", "href": "/api/products/5" }
  ]
}
```

এখানে `links` অংশটি নির্দেশ করছে, আপনি এই রিসোর্সটি দেখতে, আপডেট করতে বা ডিলিট করতে পারবেন — এই লিংকগুলো API নিজেই দিয়ে দিচ্ছে। এই অংশটাই **HATEOAS**।

---

### ❓ Is HATEOAS Required in REST?

🔸 **Technically:**
না, HATEOAS REST-এর জন্য **আবশ্যক (required)** না, তবে এটি REST-এর একটি **optional constraint**।

🔸 **Practically:**
বেশিরভাগ REST API-তে HATEOAS ব্যবহার করা হয় না কারণ এটি ইমপ্লিমেন্ট করা জটিল এবং ক্লায়েন্টের জন্য প্রয়োজন না হলে বাড়তি বোঝা হয়।

---

### ✅ সারসংক্ষেপ :

| বিষয়            | ব্যাখ্যা                                                   |
| --------------- | ---------------------------------------------------------- |
| **HATEOAS**     | API রেসপন্সের মধ্যে পরবর্তী Action-এর লিংক থাকে।           |
| **প্রয়োজনীয়তা** | REST এর জন্য বাধ্যতামূলক নয়, তবে উন্নত REST design-এর অংশ। |
| **ব্যবহার**     | বড় ও জটিল সিস্টেমে ক্লায়েন্টকে গাইড করার জন্য ব্যবহৃত হয়।  |
---

<br>

# 15. What are some best practices for designing RESTful endpoints? (e.g., resource-based URLs, plural nouns, nested routes).


RESTful API ডিজাইনে ক্লিন, স্ট্যান্ডার্ড এবং স্কেলেবল এন্ডপয়েন্ট তৈরি করতে নিচের Best Practices গুলো অনুসরণ করা উচিত।


### 📌 ১. **Use Nouns, Not Verbs**

**❌ Bad:** `GET /getAllUsers`
<br>
**✅ Good:** `GET /users`

> এক্সপ্লোরেবল ও স্ট্যান্ডার্ড রাখতে শুধু রিসোর্স (noun) ব্যবহার করুন।

---

### 📌 ২. **Use Plural Nouns for Collections**

**❌ Bad:** `/user/1` 
<br>
**✅ Good:** `/users/1`

> সাধারণত collection বোঝাতে plural (users, products) ব্যবহার করুন।

---

### 📌 ৩. **Use HTTP Methods Properly**

| Method            | Description      |
| ----------------- | ---------------- |
| `GET /users`      | সব ইউজার লিস্ট   |
| `POST /users`     | নতুন ইউজার তৈরি  |
| `GET /users/1`    | নির্দিষ্ট ইউজার  |
| `PUT /users/1`    | পুরো ইউজার আপডেট |
| `PATCH /users/1`  | আংশিক আপডেট      |
| `DELETE /users/1` | ইউজার ডিলিট      |

---

### 📌 ৪. **Use Nested Routes for Relationships**

**✅ Good:**

```http
GET /users/1/posts
POST /users/1/posts
```

> Parent-child সম্পর্ক বোঝাতে nested routes ব্যবহার করুন।

---

### 📌 ৫. **Filter, Sort, Paginate via Query Parameters**

```http
GET /products?category=electronics&sort=price_desc&page=2
```

> Query parameters দিয়ে ফিল্টারিং, সাজানো এবং pagination করুন।

---

### 📌 ৬. **Use Consistent Naming Conventions**

* সব lowercase এবং hyphen/underscore বাদ দিয়ে `/users`, `/products`
* Consistent naming structure রাখুন

---

### 📌 ৭. **Version Your API**

```http
/api/v1/users
```

> ভবিষ্যতের জন্য ভার্সন সাপোর্ট রাখুন।

---

### 📌 ৮. **Use Proper Status Codes**

| Code | Meaning      |
| ---- | ------------ |
| 200  | Success      |
| 201  | Created      |
| 400  | Bad Request  |
| 401  | Unauthorized |
| 404  | Not Found    |
| 500  | Server Error |

---

### 📌 ৯. **Avoid Actions in URLs**

**❌ Bad:** `/users/1/delete`
<br>
**✅ Good:** `DELETE /users/1`

---

### 📌 ১০. **Return Consistent Response Structure**

```json
{
  "status": "success",
  "data": { ... },
  "message": "User created successfully."
}
```

> Response format সব জায়গায় একই রাখা উচিত।

---

### ✅ সারসংক্ষেপ (বাংলায়):

> RESTful API ডিজাইন করার সময় resource ভিত্তিক plural noun ব্যবহার করুন, HTTP method অনুযায়ী কাজ করুন, nested routes ব্যবহার করুন parent-child রিলেশনের জন্য, এবং versioning, pagination, এবং সঠিক status code ফলো করুন।

---

<br>

# 16. How do you differentiate between 404 Not Found and 204 No Content?

দুটো HTTP status code — `404` ও `204` — দেখতে কিছুটা কাছাকাছি মনে হলেও, তাদের **উদ্দেশ্য ও ব্যবহার একেবারেই ভিন্ন**।

---

### ✅ `404 Not Found`

| বিষয়                 | ব্যাখ্যা                                                |
| -------------------- | ------------------------------------------------------- |
| **অর্থ**             | রিকোয়েস্ট করা রিসোর্স **পাওয়া যায়নি**                   |
| **কখন ব্যবহার হয়**   | যখন ইউজার এমন একটি রিসোর্স চায়, যা এক্সিস্ট করে না      |
| **উদাহরণ**           | `GET /products/9999` → যদি ID 9999-এর প্রোডাক্ট না থাকে |
| **Response Body**    | সাধারণত একটি error message থাকে                         |
| **Example Response** |                                                         |

```json
{
  "status": 404,
  "message": "Product not found."
}
```

---

### ✅ `204 No Content`

| বিষয়                 | ব্যাখ্যা                                                                    |
| -------------------- | --------------------------------------------------------------------------- |
| **অর্থ**             | অনুরোধ সফল হয়েছে, কিন্তু **রেসপন্সে কোনো কনটেন্ট নেই**                      |
| **কখন ব্যবহার হয়**   | যেমন: সফলভাবে কোনো ডেটা মুছে ফেলেছেন, কিন্তু রিটার্ন করার মতো কিছু নেই      |
| **উদাহরণ**           | `DELETE /products/10` → প্রোডাক্ট ডিলিট হয়েছে, কিন্তু রিটার্ন করার কিছু নেই |
| **Response Body**    | একদম ফাঁকা (empty)                                                          |
| **Example Response** |                                                                             |

```
HTTP/1.1 204 No Content
```

---

### 🔁 তুলনামূলক টেবিল:

| বৈশিষ্ট্য      | `404 Not Found`            | `204 No Content`                  |
| -------------- | -------------------------- | --------------------------------- |
| মানে           | রিসোর্স খুঁজে পাওয়া যায়নি  | রিকোয়েস্ট সফল, কিন্তু রেসপন্স নেই |
| Body           | সাধারণত error message থাকে | একদম ফাঁকা                        |
| কখন হয়         | ভুল ID বা route            | সফল update/delete ইত্যাদি         |
| Common methods | `GET`, `PUT`               | `DELETE`, `PUT`, `PATCH`          |

---

### ✅ সারসংক্ষেপ (বাংলায়):

> 🔹 `404` মানে রিসোর্সই নেই।
> 🔹 `204` মানে কাজটা ঠিকঠাক হয়েছে, কিন্তু রিটার্নে কিছু নেই।

---

<br>

# 17. How would you design an API for file upload/download ?

ফাইল আপলোড ও ডাউনলোড API ডিজাইন করতে হলে RESTful principles মেনে এবং নিরাপত্তা মাথায় রেখে API রুট, controller, validation ইত্যাদি গঠন করতে হয়।

---

## ✅ ১. File Upload API ডিজাইন

### 🔸 **Endpoint:**

```http
POST /api/files
```

### 🔸 **Request Type:**

`multipart/form-data`
(ফাইল আপলোড করার জন্য এই টাইপ দরকার হয়)

### 🔸 **Headers:**

```http
Content-Type: multipart/form-data
Authorization: Bearer <token>
```

### 🔸 **Request Body Example:**

```json
{
  "file": <attached_file>,
  "title": "profile_picture"
}
```

### 🔸 **Laravel Controller (example):**

```php
public function upload(Request $request)
{
    $request->validate([
        'file' => 'required|file|max:2048', // 2MB max
        'title' => 'nullable|string'
    ]);

    $path = $request->file('file')->store('uploads');

    return response()->json([
        'message' => 'File uploaded successfully.',
        'path' => $path
    ], 201);
}
```

---

## ✅ ২. File Download API ডিজাইন

### 🔸 **Endpoint:**

```http
GET /api/files/{filename}
```

### 🔸 **Headers (Optional):**

```http
Authorization: Bearer <token>
```

### 🔸 **Laravel Controller (example):**

```php
public function download($filename)
{
    $path = storage_path('app/uploads/' . $filename);

    if (!file_exists($path)) {
        return response()->json([
            'message' => 'File not found.'
        ], 404);
    }

    return response()->download($path);
}
```

---

## ✅ নিরাপত্তার জন্য করণীয়

1. **Authentication Middleware:** নিশ্চিত করুন শুধু অথরাইজড ইউজার ফাইল আপলোড/ডাউনলোড করতে পারবে।
2. **File Validation:** শুধুমাত্র নির্দিষ্ট file type (jpg, pdf, etc.) এবং size অনুমোদন করুন।
3. **Storage Restriction:** Public storage না করে `storage/app` বা secured path ব্যবহার করুন।
4. **File Name Handling:** Random hashed name দিয়ে সংরক্ষণ করুন যেন ইউজার URL দিয়ে guess করতে না পারে।

---

## ✅ RESTful Design Summary (বাংলায়)

| কাজ          | Method | Route                   |
| ------------ | ------ | ----------------------- |
| ফাইল আপলোড   | `POST` | `/api/files`            |
| ফাইল ডাউনলোড | `GET`  | `/api/files/{filename}` |

---

🔔 **এক্সট্রা:** চাইলে আপনি ফাইলের meta info (title, size, type, uploader) ডেটাবেজে সংরক্ষণ করে, `GET /api/files` এর মাধ্যমে লিস্ট API তৈরি করতে পারেন।

---

<br>

# 18. How do you handle long-running operations in a REST API?

> যখন কোনো অপারেশন (যেমন বড় রিপোর্ট জেনারেশন, ভিডিও প্রসেসিং, ইমেইল ব্যাচ সেন্ডিং ইত্যাদি) **অনেক সময় নেয়**, তখন সেগুলো সরাসরি HTTP response এর মধ্যে না করে ব্যাকগ্রাউন্ডে **asynchronousভাবে queue বা polling** ব্যবহার করে হ্যান্ডেল করা হয়।

---

## ✅ সমাধান


### 1. **Job Queue ব্যবহার (Asynchronous processing)**

#### ✅ কীভাবে কাজ করে:

* ক্লায়েন্ট API-তে রিকোয়েস্ট পাঠায় (POST /start-report)
* সার্ভার একটি জব তৈরি করে queue-তে পাঠিয়ে দেয়
* সাথে সাথে response দিয়ে বলে: “তোমার কাজ প্রক্রিয়াধীন”
* পরে কাজ শেষ হলে ক্লায়েন্টকে জানানো হয় (polling বা notification এর মাধ্যমে)

#### 🧠 Laravel Example:

```php
// Controller
public function generateReport(Request $request)
{
    $report = Report::create(['status' => 'processing']);
    GenerateReportJob::dispatch($report->id); // push to queue

    return response()->json([
        'message' => 'Report generation started.',
        'report_id' => $report->id,
        'status' => 'processing'
    ], 202);
}
```

---

### 2. **HTTP 202 Accepted Status Code ব্যবহার**

✅ এই status code নির্দেশ করে —

> "তোমার রিকোয়েস্ট গ্রহণ করা হয়েছে, কিন্তু এখনো প্রসেস শেষ হয়নি। পরে চেক করো।"

#### Example:

```json
{
  "status": "processing",
  "report_id": 123
}
```

---

### 3. **Client Polling (GET /status/{id})**

ক্লায়েন্ট বারবার (poll) করে রিপোর্ট রেডি কিনা চেক করতে পারে।

#### Example Route:

```http
GET /api/reports/123/status
```

#### Response:

```json
{
  "report_id": 123,
  "status": "completed",
  "download_url": "/api/reports/123/download"
}
```

---

### 4. **WebSocket / Notification (Advanced)**

কাজ শেষ হলে ক্লায়েন্টকে **পুশ নোটিফিকেশন বা ইমেইল** দিয়ে জানানো যায়।
(Laravel Notification System + Broadcast/WebSocket)

---

## ✅ সারসংক্ষেপ :

| পদ্ধতি         | ব্যাখ্যা                                     |
| -------------- | -------------------------------------------- |
| ✅ Queue        | ব্যাকগ্রাউন্ডে লম্বা কাজ প্রসেস করা          |
| ✅ 202 Accepted | সাথে সাথে কাজ শুরু হলেও পরে ফলাফল পাওয়া যাবে |
| ✅ Polling API  | ক্লায়েন্ট পরবর্তী সময়ে ফলাফল চেক করতে পারে   |
| ✅ Notification | কাজ শেষ হলে ক্লায়েন্টকে জানানো যায়           |

---

<br>

# 19. What are webhooks and how do they differ from REST APIs?


## 🔔 **What is a Webhook?**

**Webhook** হলো এক ধরনের **automatic HTTP callback**, যা কোনো ইভেন্ট ঘটলে **অন্য সার্ভারে রিকোয়েস্ট পাঠায়।**

> ✅ সহজভাবে:
> আপনি কাউকে বলে রেখেছেন – "যখন তোমার দোকানে নতুন অর্ডার হবে, আমাকে সাথে সাথে জানাবে।"

---

### ✅ Webhook-এর বৈশিষ্ট্য:

* **Push-based system** (server থেকে আপনার দিকে data পাঠানো হয়)
* Event-driven: কিছু ঘটলেই POST request করে
* Real-time update দেয় (manual polling দরকার হয় না)

#### উদাহরণ:

> Stripe/Bkash থেকে Webhook:
> যখন কোনো পেমেন্ট সফল হয়, তখন তারা আপনার সার্ভারে `/webhook/payment` রুটে POST request করে।

---

## 🔄 **What is a REST API?**

**REST API** হলো **pull-based** system — client নিজেই গিয়ে সার্ভার থেকে data চায়।

> ✅ সহজভাবে:
> আপনি নিজেই দোকানে গিয়ে বলেন – "নতুন অর্ডার হয়েছে কিনা একটু দেখাইতো।"

---

## 📊 Webhook vs REST API (Comparison Table)

| বিষয়          | Webhook                                    | REST API                    |
| ------------- | ------------------------------------------ | --------------------------- |
| Data Flow     | Push (auto)                                | Pull (manual)               |
| Trigger       | ইভেন্ট ঘটলেই                               | ইউজার অনুরোধ করলেই          |
| Communication | Server → Server                            | Client → Server             |
| Example       | Payment success, new user signup           | `GET /users`, `POST /order` |
| Use Case      | Real-time notifications                    | Resource access/control     |
| Configuration | আপনার সার্ভার URL দিয়ে সাবস্ক্রাইব করতে হয় | Client থেকে call করতে হয়    |

---

## ✅ Laravel-এ Webhook Example:

```php
// Route
Route::post('/webhook/payment', [WebhookController::class, 'handlePayment']);

// Controller
public function handlePayment(Request $request)
{
    Log::info('Payment webhook received:', $request->all());

    // পেমেন্ট স্ট্যাটাস যাচাই করে অর্ডার আপডেট
}
```

---

## সংক্ষেপে :

> 🔹 **Webhook:** অন্য সার্ভার **আপনার কাছে ডেটা পাঠায়** (পুশ করে) যখন কোনো ইভেন্ট ঘটে।
<br>
> 🔹 **REST API:** আপনি নিজের ইচ্ছায় **সার্ভার থেকে ডেটা চান** (পুল করেন)।

---

<br>

# 20. What is the N+1 query problem in REST APIs and how can you prevent it?

## ❓ What is the N+1 Query Problem?

**N+1 Query Problem** হয় তখন, যখন আপনি **একটি parent রেকর্ডের জন্য একবার query চালান**, কিন্তু প্রতিটি child রেকর্ডের জন্য **আরও আলাদা করে query** চালাতে হয়।

> 🔥 এর ফলে performance খারাপ হয় এবং **অনেক বেশি unnecessary database query** execute হয়।

---

### 🎯 উদাহরণ (Laravel):

```php
// Suppose you are fetching posts and their comments
$posts = Post::all(); // 1 query

foreach ($posts as $post) {
    echo $post->comments; // N queries (for each post)
}
```

👉 এখানে যদি 10টি পোস্ট থাকে, তাহলে **1 + 10 = 11 query** execute হবে! 😱

---

## ✅ সমাধান: Eager Loading

**Eager Loading** ব্যবহার করে আপনি parent এর সাথে child গুলো আগেই লোড করে আনতে পারেন — একদম একসাথে।

```php
$posts = Post::with('comments')->get(); // Only 2 queries
```

👉 এতে করে প্রথম query `posts` টেনে আনে, এবং দ্বিতীয় query একসাথে সব related `comments` টেনে আনে।

---

### 🔍 Example API Controller:

```php
public function index()
{
    // Without N+1 problem
    $posts = Post::with('comments.user')->get();

    return response()->json($posts);
}
```

---

## 🧠 Laravel Debugging Tip

**Debugbar**, **Clockwork**, বা `DB::listen()` দিয়ে সহজেই N+1 query চিহ্নিত করতে পারেন।

```php
\DB::listen(function ($query) {
    \Log::info($query->sql);
});
```

---

## ✅ সারসংক্ষেপ (বাংলায়):

| বিষয়              | ব্যাখ্যা                                               |
| ----------------- | ------------------------------------------------------ |
| ❌ N+1 সমস্যা      | parent একবার, কিন্তু প্রতিটি child এর জন্য আলাদা query |
| 🎯 সমাধান         | Eager Loading (`with()`, `load()`) ব্যবহার             |
| 👍 Laravel syntax | `Model::with('relation')->get()`                       |

---

> ✅ **মনে রাখুন:** যখনই আপনি REST API-তে parent-child ডেটা রিটার্ন করছেন (যেমন: post → comments), তখন `with()` দিয়ে eager load করুন, নয়তো N+1 এর ফাঁদে পড়বেন।

<br>

# 21. How would you design a REST API rate-limiting system?


## 🚦 What is Rate Limiting?

**Rate Limiting** হলো এমন একটি সিস্টেম যা ব্যবহারকারীরা নির্দিষ্ট সময়ের মধ্যে **কয়বার API কল করতে পারবে তা সীমাবদ্ধ করে**।

> 🧠 লক্ষ্য:
> সার্ভারকে ওভারলোড হওয়া থেকে বাঁচানো, abuse প্রতিরোধ করা, এবং fair usage নিশ্চিত করা।

---

## ✅ Key Elements of Rate Limiting System

| Component           | Description                                                               |
| ------------------- | ------------------------------------------------------------------------- |
| **Limit**           | নির্দিষ্ট সময়ের মধ্যে কতটি request অনুমোদন (e.g., 60 requests per minute) |
| **Identifier**      | কাকে limit করা হবে (IP address, API token, user ID)                       |
| **Window**          | Time window (per second, minute, hour, day)                               |
| **Counter Storage** | কোথায় hit count সংরক্ষণ করবেন (in-memory: Redis, DB, etc.)                |
| **Response**        | Limit ছাড়িয়ে গেলে 429 Too Many Requests status code                       |

---

## 🔧 Laravel-Based Design (Rate Limiting API)

Laravel automatically supports rate limiting via **Throttle Middleware**.

### ✅ Step 1: Define Rate Limit in `routes/api.php`

```php
Route::middleware('auth:sanctum')->group(function () {
    Route::middleware('throttle:60,1')->get('/user', function (Request $request) {
        return $request->user();
    });
});
```

🔹 `throttle:60,1` → 1 মিনিটে সর্বোচ্চ 60 টি request

---

### ✅ Step 2: Customize Rate Limit Per User

In `RouteServiceProvider.php`:

```php
use Illuminate\Cache\RateLimiting\Limit;
use Illuminate\Support\Facades\RateLimiter;

public function boot()
{
    RateLimiter::for('api', function (Request $request) {
        return Limit::perMinute(60)->by(optional($request->user())->id ?: $request->ip());
    });
}
```

---

## 🚀 Advanced Design Considerations

| Feature               | Implementation                                                  |
| --------------------- | --------------------------------------------------------------- |
| ✅ **Redis-based**     | High-performance counter using `incr` and `expire`              |
| ✅ **Sliding Window**  | More accurate tracking (vs fixed window)                        |
| ✅ **Burst handling**  | Token Bucket or Leaky Bucket algorithm                          |
| ✅ **Custom Response** | Return JSON with `Retry-After`, `X-RateLimit-Remaining` headers |

---

## 📦 Example Rate Limit JSON Response

```json
{
  "message": "Too many requests. Please slow down.",
  "retry_after": 30
}
```


## 🧠 Summary :

| বিষয়             | ব্যাখ্যা                                          |
| ---------------- | ------------------------------------------------- |
| ⛔ উদ্দেশ্য       | API abuse বা অতিরিক্ত ব্যবহার ঠেকানো              |
| 🔑 Key           | প্রতি user/token/IP অনুযায়ী limit                 |
| 🧩 প্রযুক্তি     | Laravel middleware, Redis, custom headers         |
| 📘 Best Practice | 429 status + clear message + headers ব্যবহার করুন |

---

<br>

# 22. How do you test REST APIs (unit/integration)? (e.g., tools like Postman, PHPUnit, PEST, or automated tests)


## ✅ 1. **Unit Testing**

> একক ফাংশন/মেথড আলাদা করে টেস্ট করা হয়।

### 🎯 Laravel Example (using **PEST** or **PHPUnit**):

```php
it('can return all products', function () {
    Product::factory()->count(3)->create();

    $response = $this->getJson('/api/products');

    $response->assertStatus(200)
             ->assertJsonCount(3);
});
```

📦 **টুলস**:

* `PHPUnit` (Laravel built-in)
* `PEST` (easy syntax + readable)

---

## ✅ 2. **Integration Testing**

> Controller, middleware, authentication সহ পুরো request-flow কাজ করছে কিনা তা যাচাই করা হয়।

### 🎯 Example: Authenticated API Call

```php
it('returns data for authenticated user', function () {
    $user = User::factory()->create();

    $this->actingAs($user, 'sanctum');

    $response = $this->getJson('/api/user');

    $response->assertStatus(200)
             ->assertJson([
                 'email' => $user->email,
             ]);
});
```

---

## ✅ 3. **Manual Testing with Tools**

| Tool            | Use-case                              |
| --------------- | ------------------------------------- |
| 🟠 **Postman**  | API endpoint টেস্ট ও debug করা        |
| 🔵 **Insomnia** | Postman-alternative with minimal UI   |
| 🟣 **cURL**     | Terminal থেকে API টেস্ট করার CLI tool |

### 🔧 Postman Example:

* `GET http://localhost:8000/api/products`
* Add headers, body, tokens
* View response, status code, timing

---

## ✅ 4. **Automated API Testing**

| Tool                         | Description                                              |
| ---------------------------- | -------------------------------------------------------- |
| ⚙️ PHPUnit/PEST              | Laravel built-in automation                              |
| 🧪 Laravel Dusk              | Browser-based UI testing                                 |
| 🚀 Postman Collection Runner | Multiple APIs batch test                                 |
| 🛠️ CI/CD Integration        | GitHub Actions, GitLab CI for automated testing pipeline |

---

## 🧠 সারসংক্ষেপ :

| টেস্ট টাইপ         | ব্যাখ্যা                          |
| ------------------ | --------------------------------- |
| ✅ Unit Test        | একক ফাংশন ঠিকঠাক কাজ করছে কিনা    |
| ✅ Integration Test | পুরো API flow ঠিক আছে কিনা        |
| ✅ Manual Test      | Postman/Insomnia দিয়ে API পরীক্ষা |
| ✅ Automation       | CI/CD pipeline এ test যুক্ত করা   |

---

> 🧩 Laravel Developer হিসেবে আপনি `PEST` বা `PHPUnit` ব্যবহার করে API-level integration test লিখলে confident deployment করতে পারবেন।


<br>

# 23. How would you structure a RESTful API in a microservice architecture?

Designing a **RESTful API in a Microservice Architecture** requires modular thinking, clear boundaries, and decentralized service management. Here's how you'd structure it:

---

## 🧱 1. **Split by Bounded Context (Domain-Driven Design)**

Each microservice should focus on a **single responsibility/domain**.

Example:

| Microservice      | Responsibility                         | Endpoints                                |
| ----------------- | -------------------------------------- | ---------------------------------------- |
| `User Service`    | Handles user registration, auth        | `/api/v1/users`, `/api/v1/login`         |
| `Product Service` | Manages product catalog                | `/api/v1/products`, `/api/v1/categories` |
| `Order Service`   | Processes orders                       | `/api/v1/orders`, `/api/v1/checkout`     |
| `Payment Service` | Handles payment gateway & transactions | `/api/v1/payments`                       |

---

## 🧭 2. **RESTful API Principles**

* **Resource-based URLs** (e.g., `/orders`, `/products`)
* Use **plural nouns** (`/users`, not `/user`)
* Proper use of **HTTP methods**: `GET`, `POST`, `PUT`, `DELETE`
* Use **versioning**: `/api/v1/...`

---

## 🔐 3. **Authentication & Authorization**

* Use a **centralized Auth service** (e.g., with OAuth2 or JWT)
* Services **validate tokens** but don't manage login themselves
* Each service should be **stateless** and trust the token

---

## 🔀 4. **Inter-Service Communication**

| Pattern                                  | Use                                                   |
| ---------------------------------------- | ----------------------------------------------------- |
| 🔁 REST API Calls                        | Synchronous (for real-time needs)                     |
| 📨 Message Queue (e.g., RabbitMQ, Kafka) | Asynchronous (e.g., order created → notify inventory) |
| 📬 Event-driven                          | Decouple dependencies between services                |

---

## 🛡 5. **API Gateway Layer**

Instead of exposing all services directly, use an **API Gateway** (e.g., Kong, NGINX, Laravel-based Gateway) to:

* Aggregate services into a unified API
* Handle rate limiting, CORS, SSL, logging
* Forward `/api/orders` to `OrderService`, `/api/users` to `UserService`, etc.

---

## 📂 Example Folder Structure (Laravel-based Microservice)

Each service is its own Laravel project:

```
/user-service
  /routes/api.php
  /app/Http/Controllers/UserController.php
  /tests/Feature/UserTest.php

/order-service
  /routes/api.php
  /app/Http/Controllers/OrderController.php

/api-gateway
  /routes/web.php (reverse proxy to services)
```

---

## ⚙️ Tools for Building Microservices with REST APIs

| Purpose           | Tools                               |
| ----------------- | ----------------------------------- |
| API Gateway       | Kong, Traefik, NGINX, Laravel Proxy |
| Auth              | Laravel Passport, JWT               |
| Service Discovery | Consul, Eureka                      |
| Async Messaging   | RabbitMQ, Kafka                     |
| Logging           | ELK Stack, Graylog                  |
| Monitoring        | Prometheus, Grafana                 |

---

## 🧠 Summary (Bangla):

| বিষয়                                         | ব্যাখ্যা                               |
| -------------------------------------------- | -------------------------------------- |
| 🔹 Microservice আলাদা আলাদা দায়িত্বে ভাগ করা | যেমন User, Order, Product              |
| 🔹 প্রতিটা সার্ভিসের API আলাদা               | Resource-based route + versioning      |
| 🔹 Auth আলাদা সার্ভিসে                       | যেমন JWT ব্যবহার করে token issue করা   |
| 🔹 Inter-service call                        | REST (sync) বা message queue (async)   |
| 🔹 API Gateway                               | এক জায়গায় সব সার্ভিস একসাথে expose করা |

---

<br>
<br>

<div align="center"><strong>─────── ✦ x ✦ ───────</strong></div>

<br>
<br>



# Q: How do you handle API versioning in Laravel?

Laravel-এ **API versioning** একটি খুব গুরুত্বপূর্ণ concept, বিশেষ করে যখন আপনি আপনার API নিয়মিত update করেন — কিন্তু পুরোনো version গুলোকেও support করতে চান।

এটি মূলত এমন একটি কৌশল, যার মাধ্যমে আপনার API-এর বিভিন্ন version (v1, v2, v3...) আলাদাভাবে manage করতে পারেন, যাতে পুরাতন client-রা ভেঙে না যায়।

---

## 🧩 API Versioning কেন দরকার?

* ✅ পুরোনো client/app কে ব্রেক না করেই নতুন features যুক্ত করা যায়
* ✅ Backward compatibility বজায় রাখা যায়
* ✅ Maintenance ও debug সহজ হয়
* ✅ Smooth migration path provide করা যায়

---

## ✅ Laravel-এ API Versioning কিভাবে করবেন?

Laravel-এ আমরা সাধারণত **Route based versioning** ব্যবহার করি।

---

### 🧱 Step-by-Step Implementation

### ✅ 1. Route Structure:

**routes/api.php** ফাইলে version অনুযায়ী আলাদা করে group করা হয়।

```php
// routes/api.php

use App\Http\Controllers\Api\V1\UserController as V1UserController;
use App\Http\Controllers\Api\V2\UserController as V2UserController;

Route::prefix('v1')->group(function () {
    Route::get('/users', [V1UserController::class, 'index']);
});

Route::prefix('v2')->group(function () {
    Route::get('/users', [V2UserController::class, 'index']);
});
```

---

### ✅ 2. Controller Structure:

```bash
app/
└── Http/
    └── Controllers/
        └── Api/
            ├── V1/
            │   └── UserController.php
            └── V2/
                └── UserController.php
```

প্রতিটি version আলাদা folder-এ রাখা হয়, যাতে আলাদা logic handle করা যায়।

---

### ✅ 3. Example Controller (v1)

```php
// app/Http/Controllers/Api/V1/UserController.php

namespace App\Http\Controllers\Api\V1;

use App\Http\Controllers\Controller;
use App\Models\User;

class UserController extends Controller
{
    public function index()
    {
        return response()->json([
            'version' => 'v1',
            'data' => User::all()
        ]);
    }
}
```

### ✅ 4. Example Controller (v2)

```php
// app/Http/Controllers/Api/V2/UserController.php

namespace App\Http\Controllers\Api\V2;

use App\Http\Controllers\Controller;
use App\Models\User;

class UserController extends Controller
{
    public function index()
    {
        return response()->json([
            'version' => 'v2',
            'data' => User::select('id', 'name')->get()
        ]);
    }
}
```

---

## 🔀 Bonus: Header Based Versioning (Advanced)

* যদি `Accept: application/vnd.myapp.v1+json` এর মতো custom header দিয়ে version নির্ধারণ করতে চান, middleware ব্যবহার করে detect করা যায়।

---

## 🧠 উপকারিতা:

| সুবিধা                          | ব্যাখ্যা                                             |
| ------------------------------- | ---------------------------------------------------- |
| 🔁 আলাদা Controller per version | Easy maintainability                                 |
| 🧪 Test করা সহজ                 | Version isolation ফলে নির্দিষ্ট version test করা যায় |
| ⚙️ Deployment flexible          | নতুন feature release পুরোনো API ভেঙে না দিয়েই হয়     |

---

## ✅ উপসংহার:

Laravel API versioning best practice:

| Technique                   | Use-case                      |
| --------------------------- | ----------------------------- |
| `Route::prefix('v1')`       | সবচেয়ে জনপ্রিয় ও সহজ পদ্ধতি   |
| Controller per version      | Clean separation              |
| Middleware বা Header detect | Advanced approach             |
| Subdomain versioning        | Optional (api.v1.example.com) |

---


<br>

<div align="center"><strong>─────── ✦ x ✦ ───────</strong></div>

<br>

# Q : 12.What are resource controllers, and how are they beneficial for RESTful APIs?

Laravel-এ **Resource Controllers** হলো এমন একধরনের controller যেটা automatically RESTful API-এর common CRUD (Create, Read, Update, Delete) method গুলো handle করার জন্য প্রস্তুত থাকে।

---

## 🧩 Resource Controller কী?

Laravel resource controller এমন একটা controller structure, যেখানে নিচের 7টি method আগে থেকেই define করা থাকে:

| Method         | HTTP      | URI                 | কাজ                         |
| -------------- | --------- | ------------------- | --------------------------- |
| `index()`      | GET       | /resource           | সব data দেখানো              |
| `create()`     | GET       | /resource/create    | নতুন form দেখানো            |
| `store()`      | POST      | /resource           | নতুন item সংরক্ষণ           |
| `show($id)`    | GET       | /resource/{id}      | একটি নির্দিষ্ট item দেখানো  |
| `edit($id)`    | GET       | /resource/{id}/edit | নির্দিষ্ট item-এর edit form |
| `update($id)`  | PUT/PATCH | /resource/{id}      | item update                 |
| `destroy($id)` | DELETE    | /resource/{id}      | item delete করা             |

---

## ✅ কিভাবে তৈরি করবেন?

```bash
php artisan make:controller PostController --resource
```

> এটি `app/Http/Controllers/PostController.php` ফাইলে সব ৭টি method সহ controller তৈরি করবে।

---

## ✅ Route define করার নিয়ম

```php
// routes/web.php অথবা routes/api.php

Route::resource('posts', PostController::class);
```

এই এক লাইন দিয়ে উপরোক্ত সব ৭টি route automatically generate হয়ে যাবে।

---

## ✨ উপকারিতা (Benefits):

| সুবিধা                      | ব্যাখ্যা                                     |
| --------------------------- | -------------------------------------------- |
| ✅ RESTful Convention অনুসরণ | Standard HTTP verbs (GET, POST, PUT, DELETE) |
| ✅ কোড কম                    | এক লাইনে multiple route                      |
| ✅ Maintainability           | Clean and structured controller              |
| ✅ Scalability               | আলাদা আলাদা CRUD logic handle সহজ            |
| ✅ Documentation Friendly    | Predictable route path ও methods থাকে        |

---

## 🧪 Example: `PostController`

```php
public function index() {
    return Post::all();
}

public function store(Request $request) {
    return Post::create($request->all());
}

public function show($id) {
    return Post::findOrFail($id);
}

public function update(Request $request, $id) {
    $post = Post::findOrFail($id);
    $post->update($request->all());
    return $post;
}

public function destroy($id) {
    Post::destroy($id);
    return response()->json(['message' => 'Deleted']);
}
```

---

## 🧠 Bonus Tips:

* তুমি চাইলে শুধুমাত্র কিছু method এর জন্য resource controller limit করতে পারো:

```php
Route::resource('posts', PostController::class)->only(['index', 'store']);
```

* অথবা exclude করতে পারো:

```php
Route::resource('posts', PostController::class)->except(['create', 'edit']);
```

---

<br>

<div align="center"><strong>─────── ✦ x ✦ ───────</strong></div>

<br>