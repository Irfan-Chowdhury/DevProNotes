<div align='center'>

# Nextjs  Interview Question
</div>

## 📚 Table of Contents

1. [How does Next.js differ from a traditional React application?]()
2. [What are the advantages of using Next.js for server-side rendering?]()
3. [Explain the difference between SSR and SSG.]()
4. [What is the getStaticProps function in Next.js?]()
5. [What is the getServerSideProps function in Next.js?]()
6. [What is the purpose of the next.config.js file?]()
7. [What are some common performance optimization techniques in Next.js?]()
8. [Explain how middleware works in Next.js.]()
9. [What is prefetching in Next.js?]()
10. [How can you handle client-side navigation in Next.js?]()

<br>




<br><div align="center"><strong>─────── ✦ x ✦ ───────</strong></div><br><br>

# 1. How does Next.js differ from a traditional React application?

### Next.js আর Traditional React Application-এর পার্থক্য কী?

**Next.js** হলো React-এর উপর তৈরি একটি **framework**।
আর **Traditional React app** (যেমন Create React App বা Vite) হলো মূলত **client-side React**।

নিচে পরিষ্কারভাবে পার্থক্যটা বোঝানো হলো।

---

## 🔹 Traditional React Application কীভাবে কাজ করে?

Traditional React app সাধারণত **Client-Side Rendering (CSR)** ব্যবহার করে।

👉 Flow:

1. ব্রাউজার একটা খালি HTML পায়
2. JavaScript ডাউনলোড হয়
3. React render হয়
4. তারপর data আসে ও UI দেখায়

### সমস্যা:

* প্রথম load ধীর হতে পারে
* SEO ভালো হয় না (search engine শুরুতে content পায় না)

---

## 🔹 Next.js কীভাবে আলাদা?

Next.js একাধিক rendering পদ্ধতি দেয়:

### ✅ Server-Side Rendering (SSR)

Page load হওয়ার সময়ই server থেকে HTML তৈরি হয়।

👉 SEO ভালো
👉 First load দ্রুত

---

### ✅ Static Site Generation (SSG)

Build time-এ HTML তৈরি হয়।

👉 খুব দ্রুত
👉 Blog, marketing site-এর জন্য ideal

---

### ✅ Client-Side Rendering (CSR)

প্রয়োজনে Next.js-এ CSR-ও করা যায়।

---

## 🧠 মূল পার্থক্য এক নজরে

| বিষয়               | Traditional React     | Next.js             |
| ------------------ | --------------------- | ------------------- |
| Rendering          | শুধু CSR              | SSR, SSG, CSR       |
| SEO                | দুর্বল                | খুব ভালো            |
| Routing            | Manual (React Router) | File-based routing  |
| Backend API        | আলাদা server দরকার    | Built-in API routes |
| Performance        | মাঝারি                | বেশি optimized      |
| Image optimization | Manual                | Built-in            |
| Code splitting     | Manual                | Automatic           |

---

## 🔹 Routing পার্থক্য

**Traditional React**:

```jsx
<BrowserRouter>
  <Route path="/about" element={<About />} />
</BrowserRouter>
```

**Next.js**:

```text
pages/about.js → /about
```

👉 ফাইলের নামই route

---

## 🔹 Backend সুবিধা

Next.js-এ **API Routes** থাকে:

```js
// pages/api/users.js
export default function handler(req, res) {
  res.json({ users: [] });
}
```

👉 আলাদা backend ছাড়া ছোট API বানানো যায়

---

## 🔹 Performance কেন ভালো?

* Automatic code splitting
* Image optimization
* Pre-rendering

সবকিছু built-in।

---

## ⭐ সংক্ষেপে এক লাইনে

* **Traditional React** → শুধু frontend, CSR ভিত্তিক
* **Next.js** → full-stack React framework, SEO ও performance-এর জন্য শক্তিশালী

বড়, production-level অ্যাপের জন্য আজকাল **Next.js বেশি ব্যবহার করা হয়**।



<br><div align="center"><strong>─────── ✦ x ✦ ───────</strong></div><br><br>

# 2. What are the advantages of using Next.js for server-side rendering?

### Server-Side Rendering (SSR) এর জন্য **Next.js** ব্যবহার করার সুবিধা কী?

Next.js-এ **Server-Side Rendering (SSR)** ব্যবহার করলে page-এর HTML **server-এ তৈরি হয়ে** user-এর browser-এ আসে। এর ফলে performance, SEO এবং user experience অনেক ভালো হয়।

---

## 🔹 1️⃣ SEO অনেক ভালো হয়

SSR-এ:

* Search engine সম্পূর্ণ HTML content পায়
* JavaScript load হওয়ার জন্য অপেক্ষা করতে হয় না

👉 Blog, e-commerce, news site-এর জন্য খুবই গুরুত্বপূর্ণ।

---

## 🔹 2️⃣ First Page Load দ্রুত হয়

User প্রথমবার page খুললেই—

* Server থেকে ready HTML আসে
* Blank screen কম দেখা যায়

👉 Slow internet বা low-end device-এও ভালো কাজ করে।

---

## 🔹 3️⃣ Social Media Sharing ঠিকভাবে কাজ করে

SSR-এ:

* Meta tags (`title`, `description`, `og:image`) server থেকেই আসে

👉 Facebook, LinkedIn-এ link share করলে সঠিক preview দেখা যায়।

---

## 🔹 4️⃣ Dynamic data সহজে handle করা যায়

User-specific data যেমন:

* logged-in user info
* dashboard data

SSR দিয়ে request অনুযায়ী page বানানো যায়।

```js
export async function getServerSideProps() {
  const data = await fetchData();
  return { props: { data } };
}
```

---

## 🔹 5️⃣ Security কিছুটা ভালো

* Sensitive logic server-এ থাকে
* API key বা secret client-এ expose হয় না

---

## 🔹 6️⃣ No extra setup লাগে না

Traditional React-এ SSR করতে হলে:

* আলাদা Node server
* জটিল configuration

Next.js-এ:

* SSR built-in
* minimal setup

---

## 🔹 7️⃣ Better user experience

* Page load-এর সময় কম flicker
* Content আগে দেখা যায়

👉 User retention বাড়ে।

---

## ⭐ এক লাইনে

**Next.js-এর SSR ব্যবহার করলে—
SEO ভালো হয়, page দ্রুত লোড হয়, dynamic content সহজ হয়, এবং overall user experience উন্নত হয়।**

<br><div align="center"><strong>─────── ✦ x ✦ ───────</strong></div><br><br>

# 3. Explain the difference between SSR and SSG.

### SSR (Server-Side Rendering) আর SSG (Static Site Generation) এর পার্থক্য

SSR আর SSG—দুটোই **page pre-rendering** পদ্ধতি, কিন্তু **কখন HTML তৈরি হয়**—এই জায়গাতেই মূল পার্থক্য।

---

## 🔹 SSR (Server-Side Rendering) কী?

**প্রতিবার user request এলে** server তখনই HTML তৈরি করে।

👉 “Just-in-time” rendering

```js
export async function getServerSideProps() {
  return { props: {} };
}
```

### বৈশিষ্ট্য

* প্রতিটি request-এ নতুন HTML
* User-specific data দেখানো যায়
* Server-এ বেশি কাজ হয়

### ব্যবহার করবেন যখন:

* Dashboard
* Logged-in user data
* Real-time / frequently changing content

---

## 🔹 SSG (Static Site Generation) কী?

**Build time-এ একবার HTML তৈরি হয়**, তারপর সবাই সেই একই HTML পায়।

👉 “Build-time rendering”

```js
export async function getStaticProps() {
  return { props: {} };
}
```

### বৈশিষ্ট্য

* HTML আগে থেকেই তৈরি
* খুব দ্রুত load হয়
* Server load প্রায় নেই

### ব্যবহার করবেন যখন:

* Blog
* Marketing site
* Documentation
* Content কম বদলায়

---

## 🧠 মূল পার্থক্য এক নজরে

| বিষয়         | SSR             | SSG          |
| ------------ | --------------- | ------------ |
| HTML তৈরি হয় | প্রতি request-এ | Build time-এ |
| Speed        | তুলনামূলক ধীর   | খুব দ্রুত    |
| SEO          | ভালো            | খুব ভালো     |
| Dynamic data | খুব ভালো        | সীমিত        |
| Server load  | বেশি            | কম           |
| Hosting cost | বেশি            | কম           |

---

## 🔹 ISR (এক লাইনে)

Next.js-এ **ISR (Incremental Static Regeneration)** আছে—
SSG + নির্দিষ্ট সময় পর update।

```js
revalidate: 60
```

---

## ⭐ এক লাইনে

* **SSR** → প্রতিবার request-এ HTML তৈরি (dynamic content)
* **SSG** → build time-এ HTML তৈরি (fast & static content)

সঠিক পছন্দ নির্ভর করে—
👉 **ডেটা কত ঘন ঘন বদলায় তার উপর**


<br><div align="center"><strong>─────── ✦ x ✦ ───────</strong></div><br><br>

# 4. What is the getStaticProps function in Next.js?


**`getStaticProps`** হলো Next.js-এর একটি special function,
যেটা ব্যবহার করা হয় **Static Site Generation (SSG)** করার জন্য।

সহজভাবে বললে—
👉 **build time-এ data এনে HTML তৈরি করে রাখে**।

---

## 🔹 `getStaticProps` কীভাবে কাজ করে?

* এই function **server-এ চলে**, browser-এ না
* build করার সময় API / database থেকে data আনে
* সেই data দিয়ে page-এর HTML আগেই বানিয়ে ফেলে

```js
export async function getStaticProps() {
  const res = await fetch("https://api.example.com/posts");
  const posts = await res.json();

  return {
    props: {
      posts,
    },
  };
}
```

👉 এই page build হওয়ার সময়ই ready হয়ে যায়।

---

## 🔹 কখন ব্যবহার করবেন?

`getStaticProps` ব্যবহার করবেন যখন:

* Data খুব ঘন ঘন বদলায় না
* SEO গুরুত্বপূর্ণ
* Page খুব দ্রুত load করতে চান

যেমন:

* Blog page
* News article (দিনে ১–২ বার update)
* Marketing / landing page
* Documentation site

---

## 🔹 এর সুবিধা

* 🚀 Page খুব দ্রুত load হয়
* 🔍 SEO খুব ভালো হয়
* 🧾 Server-এ প্রতি request-এ কাজ করতে হয় না
* 💰 Hosting cost কম হয়

---

## 🔹 ISR (Incremental Static Regeneration)

Static হলেও নির্দিষ্ট সময় পর update করা যায়:

```js
return {
  props: { posts },
  revalidate: 60, // 60 সেকেন্ড পর নতুন build
};
```

---

## ⚠️ গুরুত্বপূর্ণ বিষয়

* `getStaticProps` শুধু **page file-এ** ব্যবহার করা যায়
* Client component-এ ব্যবহার করা যায় না
* `window`, `document` এখানে পাওয়া যাবে না

---

## ⭐ এক লাইনে

**`getStaticProps` ব্যবহার করা হয় Next.js-এ page-কে build time-এ static HTML বানানোর জন্য, যাতে page দ্রুত, SEO-friendly ও efficient হয়।**


<br><div align="center"><strong>─────── ✦ x ✦ ───────</strong></div><br><br>

# 5. What is the getServerSideProps function in Next.js?

### Next.js-এ **`getServerSideProps`** কী?

**`getServerSideProps`** হলো Next.js-এর একটি special function,
যেটা ব্যবহার করা হয় **Server-Side Rendering (SSR)** করার জন্য।

সহজভাবে বললে—
👉 **প্রতিবার page request এলে server তখনই data এনে HTML তৈরি করে।**

---

## 🔹 `getServerSideProps` কীভাবে কাজ করে?

* এই function **শুধু server-এ চলে** (browser-এ না)
* **প্রতিটি request**-এ execute হয়
* API, database, cookies, headers—সব access করা যায়

```js
export async function getServerSideProps(context) {
  const res = await fetch("https://api.example.com/users");
  const users = await res.json();

  return {
    props: {
      users,
    },
  };
}
```

👉 User page খুললেই server থেকে fresh data আসে।

---

## 🔹 কখন ব্যবহার করবেন?

`getServerSideProps` ব্যবহার করবেন যখন:

* Data **প্রতিবার বদলায়**
* User-specific content দরকার
* Authentication / authorization চেক করতে হবে

যেমন:

* Dashboard
* Profile page
* Admin panel
* Order history
* Personalized content

---

## 🔹 `context` দিয়ে কী পাওয়া যায়?

`context` থেকে পাওয়া যায়:

* `req` → request (cookies, headers)
* `res` → response
* `params` → dynamic route
* `query` → URL query

👉 Login check বা role-based access এ খুব কাজে লাগে।

---

## 🔹 সুবিধা

* SEO ভালো হয়
* সবসময় latest data পাওয়া যায়
* Sensitive logic server-এ রাখা যায়

---

## ⚠️ অসুবিধা

* প্রতি request-এ server কাজ করে → তুলনামূলক ধীর
* Server cost বেশি হতে পারে

---

## ⭐ এক লাইনে

**`getServerSideProps` ব্যবহার করা হয় Next.js-এ প্রতিটি request-এর সময় server থেকে data এনে page render করার জন্য—যখন dynamic ও user-specific content দরকার।**


<br><div align="center"><strong>─────── ✦ x ✦ ───────</strong></div><br><br>

# 6. What is the purpose of the next.config.js file?

### Next.js-এ **`next.config.js`** ফাইলের উদ্দেশ্য কী?

**`next.config.js`** হলো Next.js প্রজেক্টের **configuration ফাইল**।
এই ফাইল দিয়ে আপনি Next.js-এর **ডিফল্ট আচরণ কাস্টমাইজ** করতে পারেন।

সহজভাবে বললে—
👉 *এই ফাইল বলে দেয় Next.js কীভাবে build করবে, কীভাবে run করবে, আর কী extra নিয়ম মানবে।*

---

## 🔹 `next.config.js` দিয়ে কী কী করা যায়?

### 1️⃣ Environment configuration

Build বা runtime-এ কোন সেটিংস ব্যবহার হবে তা ঠিক করা যায়।

```js
module.exports = {
  reactStrictMode: true,
};
```

---

### 2️⃣ Image optimization সেট করা

বাইরের domain থেকে image আনতে হলে এখানে অনুমতি দিতে হয়।

```js
module.exports = {
  images: {
    domains: ["images.example.com"],
  },
};
```

👉 না দিলে image load হবে না।

---

### 3️⃣ Redirect ও Rewrite

URL পরিবর্তন বা map করা যায়।

```js
module.exports = {
  redirects: async () => [
    {
      source: "/old",
      destination: "/new",
      permanent: true,
    },
  ],
};
```

---

### 4️⃣ Custom Webpack configuration

Advanced ক্ষেত্রে webpack কাস্টমাইজ করা যায়।

```js
module.exports = {
  webpack(config) {
    config.resolve.fallback = { fs: false };
    return config;
  },
};
```

---

### 5️⃣ Base path / Asset prefix

যখন app subfolder বা CDN-এ deploy করা হয়।

```js
module.exports = {
  basePath: "/app",
};
```

---

### 6️⃣ Experimental বা performance feature চালু করা

Next.js-এর নতুন feature enable করা যায়।

```js
module.exports = {
  experimental: {
    appDir: true,
  },
};
```

---

## ⚠️ গুরুত্বপূর্ণ বিষয়

* `next.config.js` **server-side file**
* এখানে করা পরিবর্তন apply করতে **server restart দরকার**
* Browser-এ এই ফাইল expose হয় না

---

## ⭐ এক লাইনে

**`next.config.js` ব্যবহার করা হয় Next.js অ্যাপের build, performance, routing, image, এবং advanced behavior কাস্টমাইজ করার জন্য।**

<br><div align="center"><strong>─────── ✦ x ✦ ───────</strong></div><br><br>

# 7. What are some common performance optimization techniques in Next.js?

### Next.js-এ common performance optimization techniques

Next.js দ্রুত করার মূল টার্গেট: **কম JS পাঠানো**, **আগে থেকেই HTML ready রাখা**, **image/network optimize করা**, আর **cache ঠিকভাবে ব্যবহার করা**।

---

## 1) SSG / ISR ব্যবহার করুন (সবচেয়ে বড় win)

* **SSG (`getStaticProps`)**: build time-এ HTML তৈরি → খুব দ্রুত
* **ISR (`revalidate`)**: নির্দিষ্ট সময় পর static page আপডেট

➡️ Blog/marketing/product listing টাইপ page-এ ideal।

---

## 2) SSR শুধু দরকার হলে ব্যবহার করুন

**`getServerSideProps`** প্রতিবার request-এ চলে → server load বাড়ে, ধীর হতে পারে।
User-specific বা frequently changing data না হলে SSR এড়ান।

---

## 3) Image optimize করুন (`next/image`)

`next/image`:

* auto resize
* lazy load
* modern formats support

```jsx
import Image from "next/image";
<Image src="/banner.jpg" width={1200} height={600} alt="banner" />
```

---

## 4) Code splitting + Dynamic import

Heavy component সবসময় load না করে দরকারে load করুন।

```js
import dynamic from "next/dynamic";
const Chart = dynamic(() => import("../components/Chart"), { ssr: false });
```

---

## 5) `next/font` ব্যবহার করুন (fonts optimize)

External font load slow হলে layout shift হয়। `next/font` optimized।

---

## 6) Bundle size কমান

* অপ্রয়োজনীয় library বাদ
* tree-shaking friendly imports
* শুধু প্রয়োজনীয় component import

Tip: Production bundle analyze করতে `@next/bundle-analyzer` ব্যবহার করা হয়।

---

## 7) Caching ঠিক করুন

* CDN caching (static assets)
* API responses caching (RTK Query / SWR)
* ISR pages cache by default

---

## 8) Prefetching (Link)

Next.js `<Link>` অনেক সময় route prefetch করে, navigation fast হয়।

```jsx
import Link from "next/link";
<Link href="/products">Products</Link>
```

---

## 9) Data fetching optimize করুন

* একাধিক API call একসাথে (Promise.all)
* server-side এ প্রয়োজনীয় data only
* client side এ debounce/throttle (search)

---

## 10) Large list হলে virtualization

অনেক item render করলে slow হয়। `react-window`/`react-virtualized` ব্যবহার করুন।

---

## ⭐ ছোট summary

* **SSG/ISR first**
* **SSR only when needed**
* **`next/image` + dynamic import**
* **bundle/caching/data-fetch optimize**

এসব ঠিকভাবে করলে Next.js অ্যাপ সাধারণত অনেক smooth ও fast হয়।


<br><div align="center"><strong>─────── ✦ x ✦ ───────</strong></div><br><br>

# 8. Explain how middleware works in Next.js.

### Next.js-এ **Middleware** কীভাবে কাজ করে?

**Middleware** হলো এমন কোড, যা **request server-এ পৌঁছানোর আগেই** চলে।
এর কাজ হলো—request **allow/deny**, **redirect**, **rewrite**, বা **modify** করা।

সহজভাবে বললে:
👉 *User → Middleware → Page / API*

![Image](https://images-www.contentful.com/fo9twyrwpveg/6p3JeZWpvNVCLFxZHZKm8L/148404ca3a5b75d83b5a3f6122742ebd/nextjs-middleware-image1.png)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2A0MwX2ehe6oa_JO8xmcsMVA%402x.jpeg)

![Image](https://www.plasmic.app/blog/static/images/nextjs-personalization/comparison-diagram.png)

---

## 🔹 Middleware কখন চলে?

* Page render হওয়ার **আগে**
* API route hit হওয়ার **আগে**
* Static file serve হওয়ার **আগে** (match করলে)

এটা **Edge Runtime**-এ চলে, তাই খুব দ্রুত।

---

## 🔹 Middleware দিয়ে কী কী করা যায়?

### ✅ Authentication / Authorization

* Login আছে কি না চেক
* Role-based access (admin/user)

### 🔁 Redirect / Rewrite

* `/login` এ পাঠানো
* পুরনো URL নতুন URL-এ map

### 🌍 Localization

* Language detect করে route বদলানো

### 🛡️ Security checks

* Token, headers, cookies যাচাই

---

## 🔹 Middleware ফাইল কোথায় থাকে?

Project root-এ **`middleware.ts`** বা **`middleware.js`**

```
/middleware.ts
```

---

## 🔹 Basic middleware উদাহরণ

```ts
import { NextResponse } from "next/server";
import type { NextRequest } from "next/server";

export function middleware(request: NextRequest) {
  const isLoggedIn = request.cookies.get("token");

  if (!isLoggedIn) {
    return NextResponse.redirect(new URL("/login", request.url));
  }

  return NextResponse.next();
}
```

👉 Login না থাকলে `/login` এ redirect হবে।

---

## 🔹 নির্দিষ্ট route-এ middleware চালানো (matcher)

```ts
export const config = {
  matcher: ["/dashboard/:path*", "/admin/:path*"],
};
```

👉 শুধু `/dashboard` ও `/admin` route-এ middleware চলবে।

---

## 🔹 Middleware কী করতে পারে না?

* Database access (সাধারণত না)
* Heavy computation
* Node-specific API (`fs`, `process`)

কারণ এটি **Edge environment**।

---

## 🧠 কখন Middleware ব্যবহার করবেন?

* Auth guard দরকার হলে
* Global redirect / rewrite দরকার হলে
* Request-level logic centralize করতে চাইলে

---

## ⭐ এক লাইনে

**Next.js Middleware হলো request-এর gatekeeper 🚦—page বা API চালুর আগেই request যাচাই, redirect বা modify করার জন্য ব্যবহার হয়।**

<br><div align="center"><strong>─────── ✦ x ✦ ───────</strong></div><br><br>

# 9. What is prefetching in Next.js?

Prefetching মানে হলো:
 👉 user যেই link-এ যেতে পারে, Next.js আগে থেকেই সেই page load করে রাখে।

next/link ব্যবহার করলে automatically prefetch হয়।
👉 Result: instant page transition


<br><div align="center"><strong>─────── ✦ x ✦ ───────</strong></div><br><br>

# 10 .How can you handle client-side navigation in Next.js?

Next.js-এ client-side navigation করা হয়:
* <Link /> component দিয়ে

* useRouter() hook দিয়ে

👉 Page reload ছাড়াই route change হয় <br>
👉 User experience smooth হয়

<br><div align="center"><strong>─────── ✦ x ✦ ───────</strong></div><br><br>
