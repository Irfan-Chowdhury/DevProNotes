<div align='center'>

# Express Js  Interview Question
</div>

## 📚 Table of Contents

1. [How to do Cross-Origin Resource Sharing in express.js?]()
2. [What are the characteristics of global error handlers?]()
3. [What are the differences between app.route() and app.use()?]()
4. [What are the uses of the Next function?]()
5. [What are the advantages and disadvantages of using middleware?]()
6. [How is JSON and URL encoded body parsing done in Express?]()
7. [How to create and use custom middleware in Express?]()
8. [What is the lifecycle of Express Middleware and how does it work?]()
9. [How are static files served in Express?]()
10. [What kind of tasks are required to configure a project in Express?]()

<br>

# 1. How to do Cross-Origin Resource Sharing in express.js?

Express.js এ **CORS (Cross-Origin Resource Sharing)** মানে হলো: আপনার API যদি `http://localhost:5000` এ চলে, আর Frontend `http://localhost:3000` থেকে সেই API কল করে—তাহলে ব্রাউজার “ভিন্ন origin” বলে ব্লক করতে পারে। CORS সেট করলে আপনি ব্রাউজারকে বলেন: “এই এই origin থেকে কল করতে দাও।”

---

## 1) সবচেয়ে সহজ উপায় (cors প্যাকেজ ব্যবহার)

**আমি এখন `cors` ব্যবহার করে সেটআপ দেখাচ্ছি—ঠিক আছে?** (আপনি বললে আমি পরের ধাপ/কোড আরও কাস্টমাইজ করে দেব।)

### Install

```bash
npm i cors
```

### Basic (সব origin allow — ডেভেলপমেন্টে ঠিক)

```js
import express from "express";
import cors from "cors";

const app = express();

app.use(cors()); // allow all origins
app.use(express.json());

app.get("/api/health", (req, res) => res.json({ ok: true }));

app.listen(5000, () => console.log("Server running on 5000"));
```

---

## 2) নির্দিষ্ট Origin allow করা (Production friendly)

শুধু আপনার Frontend domain থেকে allow করবেন:

```js
const allowedOrigins = [
  "http://localhost:3000",
  "https://your-frontend.com",
];

app.use(cors({
  origin: function (origin, callback) {
    // Postman/Server-to-server request এ origin নাও থাকতে পারে
    if (!origin) return callback(null, true);

    if (allowedOrigins.includes(origin)) return callback(null, true);

    return callback(new Error("Not allowed by CORS"));
  },
  credentials: true, // cookie/session পাঠাতে হলে
}));
```

✅ এটা বেশি সেফ।

---

## 3) Cookie / Session / JWT cookie হলে (credentials দরকার)

যদি আপনি **cookie-based auth** (session বা httpOnly cookie) ব্যবহার করেন:

```js
app.use(cors({
  origin: "http://localhost:3000",
  credentials: true,
}));
```

**খেয়াল রাখবেন**

* Frontend (fetch/axios) এ `credentials: "include"` দিতে হবে
* Cookie হলে `SameSite=None; Secure` প্রোডাকশনে লাগতে পারে (HTTPS)

---

## 4) শুধু কিছু HTTP method / headers allow করা

```js
app.use(cors({
  origin: "http://localhost:3000",
  methods: ["GET", "POST", "PUT", "DELETE"],
  allowedHeaders: ["Content-Type", "Authorization"],
}));
```

---

## 5) Preflight (OPTIONS) ইস্যু হলে

কিছু রিকুয়েস্ট আগে ব্রাউজার **OPTIONS** পাঠায় (preflight)। সাধারণত `cors()` দিলে হয়ে যায়, তবুও দরকার হলে:

```js
app.options("*", cors());
```

---

## সাধারণ ভুল (যেগুলোতে CORS কাজ করে না)

* `app.use(cors())` **routes এর পরে** লিখলে সমস্যা হতে পারে → সবসময় উপরে দিন।
* `origin: "*"` এর সাথে `credentials: true` একসাথে দিলে ব্রাউজার ব্লক করবে।
* Proxy/Load balancer থাকলে origin mismatch হতে পারে (ডোমেইন ঠিক মিলছে কিনা দেখুন)।

---

আপনি কোনটা ব্যবহার করছেন:

1. শুধু normal API call (token header) নাকি
2. cookie/session-based login?




<br><div align="center"><strong>─────── ✦ x ✦ ───────</strong></div><br><br>


# 2. What are the characteristics of global error handlers ?

**Global error handler** মানে হলো—অ্যাপের কোথাও ভুল (error) হলে, সেটাকে ধরার জন্য **একটাই সাধারণ জায়গা**। নিচে এর **মূল বৈশিষ্ট্যগুলো** খুব সহজ ভাষায় দিচ্ছি 👇

1. **এক জায়গা থেকে সব error ধরা**
   অ্যাপের যেকোনো ফাইলে error হলে, আলাদা আলাদা করে ধরতে হয় না। Global error handler সব একসাথে ধরে।

2. **একই রকম response দেয়**
   সব error হলে একই format এ message যায় (যেমন: status, message)। এতে Frontend বুঝতে সহজ হয়।

3. **কোড পরিষ্কার থাকে**
   প্রতিটা route এ try–catch লিখতে হয় না। কোড ছোট, পরিষ্কার ও পড়তে সহজ হয়।

4. **অ্যাপ ক্র্যাশ হওয়া কমে**
   Error ঠিকভাবে ধরা পড়লে সার্ভার হঠাৎ বন্ধ হয়ে যায় না।

5. **Debug করা সহজ**
   সব error এক জায়গায় লগ (console / file) করা যায়। কোন error কোথায় হচ্ছে বুঝতে সুবিধা হয়।

6. **Security বাড়ায়**
   User কে আসল system error দেখায় না। ভেতরের তথ্য লুকিয়ে রেখে safe message দেয়।

7. **Maintenance সহজ**
   Error message বা behavior বদলাতে চাইলে শুধু এক জায়গায় বদলালেই হয়।

সংক্ষেপে বললে:
👉 **Global error handler = একজন গার্ড**, যে পুরো অ্যাপের সব ভুল ধরে, গুছিয়ে সামলায়, আর ইউজারকে সুন্দরভাবে জানায়।



<br><div align="center"><strong>─────── ✦ x ✦ ───────</strong></div><br><br>


# 3. What are the differences between app.route() and app.use() ?

Express.js এ **`app.route()`** আর **`app.use()`** দেখতে একটু কাছাকাছি লাগলেও কাজ আলাদা। খুব সহজ করে বুঝাই 
---

## 1️⃣ app.route() কী?

`app.route()` ব্যবহার করা হয় **একটা নির্দিষ্ট URL (route)** এর জন্য, যেখানে একাধিক HTTP method থাকে।

মানে:
👉 **একটা রাস্তায় (URL) GET, POST, PUT সব একসাথে সাজানো**

### উদাহরণ

```js
app.route("/user")
  .get((req, res) => {
    res.send("Get user");
  })
  .post((req, res) => {
    res.send("Create user");
  })
  .put((req, res) => {
    res.send("Update user");
  });
```

### app.route() এর বৈশিষ্ট্য

* শুধু **নির্দিষ্ট route** এর জন্য কাজ করে
* একই URL এর সব method এক জায়গায় থাকে
* কোড **পরিষ্কার ও গোছানো** হয়
* Middleware না, মূলত **route handler**

---

## 2️⃣ app.use() কী?

`app.use()` ব্যবহার করা হয় **middleware** বসানোর জন্য।

মানে:
👉 **প্রতিটা request আসার পথে আগে যে কাজগুলো হবে**

### উদাহরণ

```js
app.use(express.json());

app.use((req, res, next) => {
  console.log("Request received");
  next();
});
```

### নির্দিষ্ট path এও ব্যবহার করা যায়

```js
app.use("/admin", (req, res, next) => {
  console.log("Admin area");
  next();
});
```

### app.use() এর বৈশিষ্ট্য

* **সব HTTP method** এর জন্য কাজ করে
* Middleware, যেমন:

  * authentication
  * logging
  * CORS
  * error handling
* route এর আগে বা পরে বসানো যায়
* `next()` না ডাকলে request আটকে যায়

---

## 3️⃣ মূল পার্থক্য (সহজ টেবিল)

| বিষয়        | app.route()             | app.use()                        |
| ----------- | ----------------------- | -------------------------------- |
| ব্যবহার হয়  | Route handle করতে       | Middleware বসাতে                 |
| HTTP method | আলাদা আলাদা (get, post) | সব method                        |
| Path        | নির্দিষ্ট route         | সব বা নির্দিষ্ট                  |
| next()      | লাগে না                 | লাগে                             |
| কাজের ধরন   | URL অনুযায়ী response    | request–response এর মাঝখানের কাজ |

---

## 4️⃣ খুব সহজ মনে রাখার ট্রিক 🧠

* **`app.route()` = “এই রাস্তার শেষে কী হবে”**
* **`app.use()` = “রাস্তা দিয়ে আসার পথে কী কী চেক হবে”**

---

সংক্ষেপে:
👉 **Route বানাতে `app.route()`** <br>
👉 **Middleware বানাতে `app.use()`**


<br><div align="center"><strong>─────── ✦ x ✦ ───────</strong></div><br><br>


# 4. What are the uses of the Next function?

Express.js এ **`next()` function** ব্যবহার করা হয় **request–response flow নিয়ন্ত্রণ করার জন্য**। সহজভাবে বললে, এটা বলে দেয়:

👉 “এই কাজ শেষ, এখন পরের ধাপে যাও।”

নিচে এর **মূল ব্যবহারগুলো** পরিষ্কারভাবে দিচ্ছি।

---

## 1) পরের middleware এ পাঠানো

Express এ request ধাপে ধাপে middleware দিয়ে যায়।
`next()` না ডাকলে request সেখানেই আটকে যায়।

```js
app.use((req, res, next) => {
  console.log("Middleware 1");
  next(); // পরের middleware এ যাবে
});

app.use((req, res) => {
  res.send("Hello");
});
```

---

## 2) Authentication / Permission check

শর্ত ঠিক থাকলে `next()`
না হলে response দিয়ে থামিয়ে দেওয়া

```js
function isLoggedIn(req, res, next) {
  if (req.user) {
    next(); // অনুমতি আছে
  } else {
    res.status(401).send("Unauthorized");
  }
}
```

---

## 3) Route handler এ control pass করা

একই route এ একাধিক handler থাকলে

```js
app.get(
  "/profile",
  (req, res, next) => {
    console.log("Check profile");
    next();
  },
  (req, res) => {
    res.send("User profile");
  }
);
```

---

## 4) Error handler এ পাঠানো (সবচেয়ে গুরুত্বপূর্ণ)

`next(error)` দিলে Express বুঝে নেয় এটা error
এবং সরাসরি **global error handler** এ পাঠায়

```js
app.get("/data", (req, res, next) => {
  try {
    throw new Error("Something went wrong");
  } catch (err) {
    next(err); // error handler এ যাবে
  }
});
```

Global error handler:

```js
app.use((err, req, res, next) => {
  res.status(500).json({ message: err.message });
});
```

---

## 5) Request থামানো বা চালু রাখা

* `next()` → request চলবে
* `res.send()` / `res.json()` → request শেষ
* `next()` না দিলে → request ঝুলে থাকবে

---

## সংক্ষেপে মনে রাখার নিয়ম

* `next()` = **পরের ধাপে যাও**
* `next(error)` = **error handler এ যাও**
* `next()` না ডাকলে = **request আটকে যাবে**

সংক্ষেপে এক লাইনে:
👉 **`next()` Express এর traffic signal—সবুজ দিলে এগোয়, লাল দিলে থামে, error দিলে ঘুরে যায় error handler এ।**


<br><div align="center"><strong>─────── ✦ x ✦ ───────</strong></div><br><br>

# 5. What are the advantages and disadvantages of using middleware?

Express.js-এ **middleware** ব্যবহার করলে কিছু বড় সুবিধা পাওয়া যায়, আবার কিছু সীমাবদ্ধতাও থাকে। নিচে দুটো দিকই পরিষ্কারভাবে তুলে ধরা হলো।

---

## Middleware ব্যবহারের সুবিধা (Advantages)

**১) কোড পুনঃব্যবহারযোগ্য হয়**
একই কাজ (যেমন authentication, logging, validation) বারবার লিখতে হয় না। এক middleware বহু route-এ ব্যবহার করা যায়।

**২) কোড পরিষ্কার ও গুছানো থাকে**
Business logic আর common কাজ আলাদা থাকে। ফলে route handler ছোট ও পড়তে সহজ হয়।

**৩) নিরাপত্তা বাড়ে**
Authentication, authorization, rate-limit, CORS ইত্যাদি middleware দিয়ে সহজে নিয়ন্ত্রণ করা যায়।

**৪) Error handling সহজ হয়**
Global error middleware ব্যবহার করে সব error এক জায়গায় handle করা যায়।

**৫) Request flow নিয়ন্ত্রণ করা যায়**
কোন request যাবে, কোনটা আটকে যাবে—middleware দিয়েই সিদ্ধান্ত নেওয়া যায়।

**৬) Debugging ও logging সহজ**
প্রতিটি request আসার সময় log রাখা যায়, যা সমস্যা ধরতে সাহায্য করে।

---

## Middleware ব্যবহারের অসুবিধা (Disadvantages)

**১) অতিরিক্ত middleware হলে পারফরম্যান্স কমে**
প্রতিটি request সব middleware দিয়ে গেলে response ধীর হতে পারে।

**২) Flow বোঝা কঠিন হয়ে যায়**
অনেক middleware থাকলে request কোন পথে যাচ্ছে তা বুঝতে সময় লাগে।

**৩) ভুল `next()` ব্যবহার করলে সমস্যা হয়**
`next()` না ডাকলে request আটকে যায়,
আবার ভুল জায়গায় ডাকলে একাধিক response পাঠানোর error হতে পারে।

**৪) Debugging জটিল হতে পারে**
Error কোন middleware থেকে এসেছে তা ট্র্যাক করা কঠিন হয়, যদি গঠন পরিষ্কার না থাকে।

**৫) Over-engineering এর ঝুঁকি**
ছোট কাজের জন্য অপ্রয়োজনীয় middleware বানালে কোড অযথা জটিল হয়ে যায়।

---

## সংক্ষেপে সিদ্ধান্ত

* বড় ও মাঝারি অ্যাপে → **middleware খুব উপকারী**
* ছোট/simple অ্যাপে → **কম middleware ব্যবহারই ভালো**

এক লাইনে বলা যায়:
👉 **Middleware শক্তিশালী, কিন্তু বেশি হলে ভারী। সঠিক জায়গায়, সঠিক সংখ্যায় ব্যবহার করাই বুদ্ধিমানের কাজ।**

<br><div align="center"><strong>─────── ✦ x ✦ ───────</strong></div><br><br>

# 6. How is JSON and URL encoded body parsing done in Express?

Express.js এ **JSON** আর **URL-encoded body parsing** করা হয় মূলত **request body পড়ার জন্য**।
Client (frontend / Postman) যখন data পাঠায়, Express নিজে নিজে সেটা বুঝতে পারে না—**parser middleware** লাগাতে হয়।

---

## 1) JSON body parsing কী?

যখন client এই রকম data পাঠায়:

```json
{
  "name": "Rahim",
  "age": 25
}
```

এটা সাধারণত API বা AJAX request এ আসে (`Content-Type: application/json`)।

### Express এ JSON parse করার নিয়ম

```js
import express from "express";

const app = express();

app.use(express.json()); // JSON parser
```

### ব্যবহার

```js
app.post("/user", (req, res) => {
  console.log(req.body); 
  // { name: 'Rahim', age: 25 }

  res.send("JSON data received");
});
```

➡️ `express.json()` না দিলে `req.body` হবে `undefined`।

---

## 2) URL-encoded body parsing কী?

যখন HTML form থেকে data পাঠানো হয়, তখন data আসে এই ফরম্যাটে:

```
name=Rahim&age=25
```

এটাই **URL-encoded data**
(`Content-Type: application/x-www-form-urlencoded`)

### Express এ URL-encoded parse করার নিয়ম

```js
app.use(express.urlencoded({ extended: true }));
```

### ব্যবহার

```js
app.post("/login", (req, res) => {
  console.log(req.body);
  // { name: 'Rahim', age: '25' }

  res.send("Form data received");
});
```

---

## 3) `extended: true` মানে কী?

* `extended: true` → nested object support করে
* `extended: false` → শুধু simple key-value

### উদাহরণ

```js
user[name]=Rahim&user[age]=25
```

এটা ঠিকভাবে parse হবে শুধু `extended: true` হলে।

👉 এখনকার সময় **সবসময় `true` ব্যবহার করাই ভালো**।

---

## 4) দুটো একসাথে ব্যবহার (সবচেয়ে common)

```js
app.use(express.json());
app.use(express.urlencoded({ extended: true }));
```

এতে:

* API → JSON handle হবে
* Form submit → URL-encoded handle হবে

---

## 5) কখন কোনটা দরকার?

* **React / Next / API** → `express.json()`
* **HTML form submit** → `express.urlencoded()`
* **দুটোই থাকলে** → দুটোই ব্যবহার করুন

---

## সংক্ষেপে মনে রাখার নিয়ম

* JSON data → `express.json()`
* Form data → `express.urlencoded()`
* Parser না থাকলে → `req.body` ফাঁকা

এক লাইনে:
👉 **Body parser হলো Express-এর translator—client যেভাবেই data পাঠাক, server যেন সেটা বুঝতে পারে।**


<br><div align="center"><strong>─────── ✦ x ✦ ───────</strong></div><br><br>

# 7. How to create and use custom middleware in Express?

Express.js এ **custom middleware** বানানো মানে হলো—আপনি নিজের প্রয়োজন অনুযায়ী **request–response এর মাঝখানে চলা একটা function** তৈরি করা।

---

## 1) Custom middleware কী?

Custom middleware হলো একটি **function**, যার তিনটা জিনিস থাকে:

```js
(req, res, next)
```

* `req` → request এর তথ্য
* `res` → response পাঠানোর জন্য
* `next` → পরের ধাপে যাওয়ার জন্য

---

## 2) সবচেয়ে সহজ custom middleware তৈরি

### উদাহরণ: request আসলেই log দেখাবে

```js
function logger(req, res, next) {
  console.log("Request URL:", req.url);
  next(); // পরের middleware বা route এ যাবে
}
```

### ব্যবহার

```js
app.use(logger);
```

এখন **সব request** এর জন্য এই middleware চলবে।

---

## 3) নির্দিষ্ট route এ custom middleware ব্যবহার

সব জায়গায় না, শুধু নির্দিষ্ট route এ চাইলে:

```js
function checkUser(req, res, next) {
  if (req.query.user === "admin") {
    next(); // অনুমতি আছে
  } else {
    res.status(403).send("Access denied");
  }
}

app.get("/dashboard", checkUser, (req, res) => {
  res.send("Welcome to dashboard");
});
```

---

## 4) Custom authentication middleware (common use)

```js
function isAuthenticated(req, res, next) {
  const token = req.headers.authorization;

  if (token) {
    next();
  } else {
    res.status(401).json({ message: "Unauthorized" });
  }
}
```

ব্যবহার:

```js
app.get("/profile", isAuthenticated, (req, res) => {
  res.send("User profile");
});
```

---

## 5) Error handling custom middleware

Error middleware একটু আলাদা—এখানে **৪টা parameter** থাকে:

```js
function errorHandler(err, req, res, next) {
  res.status(500).json({
    error: err.message
  });
}
```

সব route এর পরে বসাতে হবে:

```js
app.use(errorHandler);
```

আর error পাঠাতে:

```js
next(new Error("Something went wrong"));
```

---

## 6) Custom middleware কোথায় রাখবেন?

ভালো practice:

```
middlewares/
 ├─ logger.js
 ├─ auth.js
 └─ errorHandler.js
```

তারপর import করে ব্যবহার করবেন।

---

## 7) মনে রাখার মূল নিয়ম

* Middleware = function
* কাজ শেষে অবশ্যই `next()` বা `res.send()`
* `next()` না ডাকলে request আটকে যাবে
* Error middleware সবসময় শেষে

---

### এক লাইনের সারসংক্ষেপ

👉 **Custom middleware আপনাকে Express-এর request flow নিজের মতো করে নিয়ন্ত্রণ করার ক্ষমতা দেয়।**


<br><div align="center"><strong>─────── ✦ x ✦ ───────</strong></div><br><br>

# 8. What is the lifecycle of Express Middleware and how does it work?

Express.js এ **middleware lifecycle** মানে হলো—একটা HTTP request আসার পর থেকে response পাঠানো পর্যন্ত **কোন কোন ধাপে middleware গুলো চলে এবং কীভাবে control একটার পর একটা এগোয়**।

নিচে পুরো flow টা পরিষ্কারভাবে ব্যাখ্যা করছি।

---

## i) Request আসে (Client → Server)

Browser / frontend / Postman থেকে request আসে Express app এ।

```
Client → Express App
```

এই সময় Express একটা **request–response cycle** শুরু করে।

---

## ii) Global middleware চলে

যেগুলো `app.use()` দিয়ে উপরে বসানো আছে, সেগুলো আগে চলে।

উদাহরণ:

```js
app.use(express.json());
app.use(loggerMiddleware);
```

Flow:

```
Request → JSON parser → Logger
```

প্রতিটা middleware:

* `req` পরিবর্তন করতে পারে
* `res` প্রস্তুত করতে পারে
* `next()` ডাকলে পরের ধাপে পাঠায়

---

## iii) Path-based middleware

যদি middleware কোনো নির্দিষ্ট path এর জন্য হয়:

```js
app.use("/admin", adminMiddleware);
```

তাহলে শুধু `/admin` দিয়ে শুরু হওয়া request এ চলবে।

---

## iv) Route matching হয়

Express এখন request এর:

* URL
* HTTP method (GET, POST ইত্যাদি)

মিলিয়ে **route handler খোঁজে**।

```js
app.get("/users", routeMiddleware, controller);
```

এখানে execution order:

```
routeMiddleware → controller
```

---

## v) Route handler response পাঠায়

Controller সাধারণত এখানেই কাজ শেষ করে:

```js
res.json({ users });
```

➡️ Response পাঠানো হলে lifecycle শেষ।

---

## vi) Error হলে flow বদলে যায়

যদি কোনো middleware বা route এ:

```js
next(error);
```

ডাকা হয়, তাহলে Express **সাধারণ middleware বাদ দিয়ে সরাসরি error middleware এ যায়**।

```js
app.use((err, req, res, next) => {
  res.status(500).json({ message: err.message });
});
```

Flow:

```
Request → middleware → error → errorHandler → Response
```

---

## vii) Middleware lifecycle এর visual flow

```
Request
  ↓
Global middleware
  ↓
Path-based middleware
  ↓
Route-level middleware
  ↓
Route handler
  ↓
Response
```

Error হলে:

```
Request
  ↓
Middleware
  ↓
Error 발생
  ↓
Error-handling middleware
  ↓
Response
```

---

## viii) Lifecycle চলার মূল নিয়ম

* Middleware **উপরে থেকে নিচে** চলে (যেভাবে লেখা)
* `next()` ডাকলে → পরের middleware
* `res.send()` দিলে → lifecycle শেষ
* `next(err)` দিলে → error lifecycle শুরু

---

## সংক্ষেপে এক লাইনে

👉 **Express middleware lifecycle হলো একটা controlled pipeline—request ঢোকে, ধাপে ধাপে process হয়, তারপর response বের হয়।**


<br><div align="center"><strong>─────── ✦ x ✦ ───────</strong></div><br><br>

# 9. How are static files served in Express ?

Express.js এ **static files** মানে হলো—যেসব ফাইল **সরাসরি server থেকে পাঠানো হয়**, কোনো logic বা controller ছাড়াই।
যেমন: **HTML, CSS, JS, image, font, PDF** ইত্যাদি।

---

## 1) Static file কীভাবে serve করা হয়?

Express এ এর জন্য built-in middleware আছে:

```js
express.static()
```

---

## 2) Basic setup (সবচেয়ে common)

ধরা যাক আপনার প্রজেক্টে এই structure আছে:

```
project/
 ├─ public/
 │   ├─ style.css
 │   ├─ app.js
 │   └─ logo.png
 └─ app.js
```

### app.js

```js
import express from "express";
const app = express();

app.use(express.static("public"));

app.listen(3000, () => {
  console.log("Server running on port 3000");
});
```

এখন ব্রাউজারে:

* `http://localhost:3000/style.css`
* `http://localhost:3000/logo.png`

➡️ ফাইলগুলো সরাসরি পাওয়া যাবে।

---

## 3) Browser এ কীভাবে কাজ করে?

Browser যখন বলে:

```
GET /style.css
```

Express দেখে:

* `public/style.css` আছে কি না
* থাকলে → ফাইল পাঠিয়ে দেয়
* না থাকলে → পরের middleware এ যায়

---

## 4) নির্দিষ্ট URL prefix দিয়ে serve করা

আপনি চাইলে `/static` দিয়ে access করাতে পারেন:

```js
app.use("/static", express.static("public"));
```

এখন:

* `http://localhost:3000/static/style.css`
* `http://localhost:3000/static/logo.png`

---

## 5) একাধিক static folder ব্যবহার

```js
app.use(express.static("public"));
app.use(express.static("uploads"));
```

Express প্রথমে `public` এ খুঁজবে, না পেলে `uploads` এ দেখবে।

---

## 6) HTML ফাইল serve করা (static ভাবে)

```js
app.use(express.static("public"));
```

`public/index.html` থাকলে:

```
http://localhost:3000/
```

খুললেই সেই HTML দেখাবে।

---

## 7) কখন static files ব্যবহার করবেন?

* CSS / JS / image
* Frontend build (React build, Vite dist)
* Public download file
* Landing page HTML

---

## 8) গুরুত্বপূর্ণ নিয়ম

* `express.static()` **উপরে** রাখতে হয়
* Static file এ `next()` লাগে না
* Static file এ controller দরকার নেই
* Security দরকার হলে sensitive ফাইল static করবেন না

---

## সংক্ষেপে এক লাইনে

👉 **`express.static()` হলো Express এর file server—যে ফাইল আছে, সেটাই সরাসরি পাঠায়।**


<br><div align="center"><strong>─────── ✦ x ✦ ───────</strong></div><br><br>

# 10. What kind of tasks are required to configure a project in Express?

Express.js এ একটি প্রজেক্ট **configure** করতে মানে হলো—শুরু থেকে অ্যাপটাকে এমনভাবে সেট করা যেন সেটা **ঠিকভাবে চলে, নিরাপদ থাকে, আর ভবিষ্যতে বাড়ানো সহজ হয়**। নিচে প্রয়োজনীয় কাজগুলো ধাপে ধাপে বোঝানো হলো।

---

## i) Project initialize করা

* Node.js project শুরু করা
* `package.json` তৈরি
* প্রয়োজনীয় dependency ইনস্টল করা

উদাহরণ:

```bash
npm init -y
npm install express
```

---

## ii) Basic app setup

* Express app তৈরি
* Server port সেট করা

```js
import express from "express";
const app = express();

app.listen(3000);
```

---

## iii) Middleware configure করা

* JSON body parser
* URL-encoded parser
* CORS
* Custom middleware

```js
app.use(express.json());
app.use(express.urlencoded({ extended: true }));
```

---

## iv) Routing structure তৈরি

* Route file আলাদা করা
* Controller pattern ব্যবহার করা

```
routes/
 ├─ user.routes.js
controllers/
 └─ user.controller.js
```

---

## v) Static files setup

* `public` বা `uploads` folder serve করা

```js
app.use(express.static("public"));
```

---

## vi) Environment configuration

* `.env` file ব্যবহার
* Port, DB URL, secret key আলাদা রাখা

```bash
npm install dotenv
```

```js
import "dotenv/config";
```

---

## vii) Error handling setup

* 404 handler
* Global error middleware

```js
app.use((req, res) => {
  res.status(404).send("Not Found");
});
```

---

## viii) Security configuration

* HTTP headers নিরাপদ করা
* Rate limiting
* Input validation

(প্রজেক্ট অনুযায়ী)

---

## ix) Database connection

* MongoDB / MySQL / PostgreSQL connect
* Connection error handle করা

---

## x) Development tools setup

* `nodemon`
* Logging
* Linting (optional)

---

## xi) Production readiness

* Build config
* Process manager (PM2)
* Error logging
* Graceful shutdown

---

## সংক্ষেপে এক লাইনে

👉 **Express project configuration মানে হলো: structure + middleware + routing + security + error handling + environment—সবকিছু ঠিকভাবে সেট করা।**

<br><div align="center"><strong>─────── ✦ x ✦ ───────</strong></div><br><br>
