আমি এখন কিছু execute করছি না—শুধু ইন্টারভিউ-ফোকাসড বাংলা ব্যাখ্যা + ছোট উদাহরণ দিচ্ছি।

---

## 1) late static binding (static:: vs self::) — কেন গুরুত্বপূর্ণ?

**`self::`** সবসময় **যে ক্লাসে লেখা হয়েছে** (parent/বর্তমান ক্লাস) সেটাকেই ধরে।
**`static::`** “late static binding” ব্যবহার করে—মানে **যে ক্লাস থেকে call করা হয়েছে (child)** সেটাকে ধরে।

**কেন দরকার:** Inheritance এ child class override করলে `static::` সেই override ধরতে পারে, `self::` পারে না।

```php
class A {
  public static function who() { echo "A"; }
  public static function test() { self::who(); }   // self
}
class B extends A {
  public static function who() { echo "B"; }
}
B::test(); // Output: A (কারণ self::who() A ধরেছে)
```

```php
class A {
  public static function who() { echo "A"; }
  public static function test() { static::who(); } // static (LSB)
}
class B extends A {
  public static function who() { echo "B"; }
}
B::test(); // Output: B
```

---

## 2) pass by value vs pass by reference (&)

আমি এখন কিছু execute করছি না—শুধু সহজ করে বুঝাচ্ছি।

## Pass by value (কপি যায়)

ফাংশনে ভ্যারিয়েবলের **কপি** পাঠানো হয়।
ফাংশনের ভিতরে বদলালেও **বাইরের ভ্যারিয়েবল বদলায় না**।

```php
function addOne($x) {
  $x = $x + 1;
}

$n = 5;
addOne($n);
echo $n; // 5 (আগের মতোই)
```

ভাবুন: আপনি বন্ধুকে আপনার নোটের **ফটোকপি** দিলেন—সে ফটোকপিতে লিখলে আপনার আসল খাতায় কিছু বদলাবে না।

---

## Pass by reference (&) (আসলটা যায়)

ফাংশনে ভ্যারিয়েবলের **আসলটা** (reference) পাঠানো হয়।
ফাংশনের ভিতরে বদলালে **বাইরের ভ্যারিয়েবলও বদলে যায়**।

```php
function addOneRef(&$x) {
  $x = $x + 1;
}

$n = 5;
addOneRef($n);
echo $n; // 6 (বদলে গেছে)
```

ভাবুন: আপনি বন্ধুকে আপনার **আসল খাতা** দিলেন—সে লিখলে আপনার খাতায়ই লেখা পড়বে।

---

## মনে রাখার ছোট নিয়ম

* **Value** = কপি → বাইরে বদলায় না ✅
* **Reference (&)** = আসল → বাইরে বদলায় ✅

**কখন & ব্যবহার করবেন?**
যখন ফাংশনের কাজই হচ্ছে বাইরের ভ্যারিয়েবলকে পরিবর্তন করা (যেমন swap, update)।


## 3) try এর ভিতরে return থাকলেও finally থাকলে কী হয়?

আমি এখন কিছু execute করছি না—শুধু সহজভাবে বুঝাচ্ছি।

## try এর ভিতরে return থাকলেও finally থাকলে কী হয়?

**finally সবসময় চলবে**—return থাকলেও, exception থাকলেও।

```php
function demo() {
  try {
    return "A";
  } finally {
    echo "FINALLY\n";
  }
}

echo demo();
```

**Output হবে:**

```
FINALLY
A
```

মানে: আগে `finally` রান করবে, তারপর `return` এর ভ্যালু রিটার্ন হবে।

---

## তাহলে finally কখন ব্যবহার করবো?

**finally ব্যবহার করবেন যখন “যাই হোক না কেন এই কাজটা শেষেই করতেই হবে”**—success হোক বা error হোক।

সবচেয়ে কমন ব্যবহার:

### 1) Resource cleanup (খুব গুরুত্বপূর্ণ)

* file খুলে কাজ করলে শেষে close করা
* lock নিলে শেষে unlock করা
* temporary file বানালে শেষে delete করা
* DB transaction begin করলে শেষে commit/rollback নিশ্চিত করা

**উদাহরণ (concept):**

```php
$fp = fopen("data.txt", "r");
try {
  // read/process
} finally {
  fclose($fp); // যাই হোক, close করতেই হবে
}
```

### 2) Transaction safe রাখা

```php
DB::beginTransaction();
try {
   // multiple DB operations
   DB::commit();
} catch (Throwable $e) {
   DB::rollBack();
   throw $e;
} finally {
   // optional: release lock / log timing etc.
}
```

### 3) Logging / timing (always run)

কোনো কাজ কত সময় নিল—error হলেও log করতে চান।

---

### ইন্টারভিউতে বলার মতো ১ লাইন

**“finally আমি ব্যবহার করি cleanup/rollback/closing কাজগুলোর জন্য—যেগুলো error হলেও অবশ্যই execute হওয়া দরকার।”**

একটা ছোট trick: `finally` এর ভেতরে সাধারণত **return দেয়া ঠিক না**—কারণ এটা try/catch এর return override করে ফেলতে পারে।


## 4) exceptions vs errors in modern PHP (Throwable)

Modern PHP (7+) এ:

* **Exception** = সাধারণভাবে অ্যাপের “expected exceptional” সমস্যা (business/validation/logic related)।
* **Error** = language/runtime-level সমস্যা (TypeError, ParseError, etc.)

দুটোই implement করে **`Throwable`**। তাই catch করতে পারেন:

```php
try {
  // code
} catch (Throwable $e) {
  // Exception বা Error দুটোই ধরবে
}
```

**ইন্টারভিউ পয়েন্ট:** production এ global handler দিয়ে Throwable log করা হয়, কিন্তু সব সময় swallow করা ঠিক না।

---

## 5) private vs protected — কখন কোনটা?

* **private:** শুধু ওই ক্লাসের ভিতরে। child class থেকেও access করা যাবে না।
* **protected:** ওই ক্লাস + child class access করতে পারবে।


**কখন private:** শক্ত encapsulation দরকার, child কে change করতে দিতে চান না। <br>
**কখন protected:** inheritance/design করা, child ক্লাসকে ব্যবহার/override করতে দিতে চান।

---

## 6) clone কীভাবে কাজ করে? কখন `__clone()` লাগে?

`clone $obj` দিলে **shallow copy** হয়—object-এর property গুলো কপি হয়, কিন্তু ভেতরে অন্য object থাকলে সেটা একই reference থাকতে পারে।

`__clone()` লাগে যখন আপনি:

* clone করার সময় extra কাজ করতে চান
* deep copy করতে চান (nested object আলাদা করে clone)

```php
class A {
  public object $inner;
  public function __clone() {
    $this->inner = clone $this->inner; // deep copy
  }
}
```

---

## 7) magic methods (__invoke, __call, __toString) — কেন ব্যবহার?

* **`__invoke()`**: object কে function এর মতো call করা যায়।

  * Use: callable service, pipeline, handler
* **`__call($name,$args)`**: non-existing method call হলে ধরবে।

  * Use: dynamic methods, proxy, wrapper (খুব সাবধানে)
* **`__toString()`**: object কে string হিসেবে ব্যবহার করলে কী হবে।

  * Use: value object display, logging

উদাহরণ:

```php
class Greeter {
  public function __invoke($name){ return "Hi $name"; }
}
$g = new Greeter();
echo $g("Monjur"); // Hi Monjur
```

**ইন্টারভিউ টিপ:** magic method overuse করলে maintain/debug কঠিন—justify করতে হয়।

---

## 8) Laravel: local এ কাজ করে, server এ fails (storage symlink / permissions) কেন?

Common কারণ:

1. **`public/storage` symlink নেই** (local এ আছে, server এ নেই)

   * `php artisan storage:link`
2. **Permission সমস্যা**: `storage/` এবং `bootstrap/cache` writable না

   * web server user (www-data) write করতে পারছে না
3. **Wrong disk config / env**: FILESYSTEM_DISK, config cache পুরনো

   * `php artisan config:clear` / `config:cache`
4. **Case-sensitive filesystem** (Linux server)

   * file নাম `Image.JPG` vs `image.jpg` mismatch

---

## 9) Laravel: `chunk()` vs `cursor()` (memory vs streaming)

* **chunk()**: নির্দিষ্ট batch এ query করে, প্রতিবার একটি chunk memory তে নেয়।

  * Pros: controlled batches, updates safe pattern
  * Cons: chunk size বড় হলে memory বেশি
* **cursor()**: generator/streaming—একটা একটা row দেয়।

  * Pros: সবচেয়ে কম memory
  * Cons: connection দীর্ঘ সময় open থাকতে পারে, eager load/complex কাজ সাবধানে

**Rule:** huge read-only processing → `cursor()`
batch processing / update per chunk → `chunk()`

---

## 10) Database: index কিভাবে বাছবেন? tradeoff কী?

**Index বানাবেন যেসব কলামে:**

* `WHERE` এ বেশি filter হয়
* `JOIN` keys
* `ORDER BY` / `GROUP BY`
* High selectivity (অনেক unique value)

**Tradeoff:**

* Read দ্রুত ✅
* কিন্তু Write (insert/update/delete) ধীর ❌ (কারণ index আপডেট হয়)
* Storage বেশি লাগে ❌

**Composite index**: `(user_id, created_at)` — query pattern অনুযায়ী order গুরুত্বপূর্ণ।

---

## 11) Eloquent: `withCount` vs `count()` — performance

* `withCount('relation')` → একবারেই list এর সাথে relation count এনে দেয় (subquery)

  * Use: users list এ `posts_count` দেখাতে
* `count()` → আপনি আলাদা query করে total count বের করেন, অথবা per item count করলে N+1 হতে পারে

ভুল pattern:

```php
$users = User::all();
foreach($users as $u) echo $u->posts()->count(); // N+1 queries
```

সঠিক:

```php
$users = User::withCount('posts')->get(); // 1 query-ish
```

---

## 12) API: idempotent endpoint ডিজাইন কিভাবে?

**Idempotent মানে:** একই request বারবার পাঠালেও result একই থাকবে (side-effect repeat হবে না)।

উদাহরণ:

* **PUT** `/users/5` (পুরা resource replace) → বারবার দিলে same
* **PATCH** update → design করলে idempotent হতে পারে
* **POST** সাধারণত non-idempotent (নতুন তৈরি হয়)

**Trick:** Payment/Order create এ `Idempotency-Key` header ব্যবহার

* একই key এ duplicate request এ same response / no double charge.

---

## 13) Security: XSS এবং Blade এ safe escaping

**XSS**: user input থেকে `<script>` ঢুকিয়ে আপনার site এ অন্যদের browser এ malicious code চালানো।

Blade default:

* `{{ $name }}` → auto escape ✅ (safe)
* `{!! $html !!}` → raw output ❌ (dangerous)

**Rule:** user-provided content হলে `{{ }}` ব্যবহার করুন। raw HTML দরকার হলে sanitize করুন (allowed tags whitelist)।

---

## 14) slow `/products` API debug + optimize কিভাবে?

Step-by-step:

1. **Measure**: Laravel Debugbar / Telescope / logs—কোথায় সময় যাচ্ছে
2. **Check queries**: N+1 আছে কি? query count বেশি কি?
3. **Eager load**: `with()` ব্যবহার
4. **Select only needed columns**: `select('id','name','price')`
5. **Indexes**: filter/sort কলামে index
6. **Pagination**: `paginate()` / `cursorPaginate()`
7. **Caching**: popular list হলে cache (Redis/file)
8. **Avoid heavy computed attributes** per item

ইন্টারভিউতে বলার মতো: “আমি আগে query profile করব, তারপর N+1 + index + pagination + cache দিয়ে fix করব।”

---

## 15) image upload এ পুরনো image থেকে যায় — safe delete/update ডিজাইন

Best practice:

* DB তে image path রাখুন
* নতুন upload হলে:

  1. নতুন file save
  2. DB update
  3. পুরনো file delete (success হলে)

**Race-safe idea:** transaction-like flow + try/catch
**Soft approach:** old file “orphan” হলে scheduled job দিয়ে cleanup
**Also:** unique filenames (uuid), validation (mime/size)

---

## 16) “Order placed” → email + sms + stock update — কোন pattern/features?

এটা classic **Observer** idea → Laravel এ:

* **Events & Listeners**: `OrderPlaced` event
* **Queues**: email/sms async
* Stock update: sync বা queued (depending criticality)

Flow:

1. Order created
2. fire event `OrderPlaced`
3. listeners: `SendEmail`, `SendSms`, `DecrementStock`
4. heavy tasks queued

---

## 17) admin-only routes — কোথায় enforce করবেন? কেন? + Policies vs Gates

**Enforce layer (best):**

* Route level **middleware**: admin routes protect করার জন্য প্রথম gatekeeper

  * `Route::middleware('admin')->group(...)`
* Business actions এ **authorization**:

  * **Policies/Gates** দিয়ে controller/service এ check

**Why:**
Middleware → “এই রুটে ঢুকতেই পারবে না”
Policy/Gate → “এই action করতে পারবে কি?” (resource ভিত্তিক)

### Policies vs Gates

* **Policy:** model/resource-centric (User can update Post?)

  * `PostPolicy@update`
* **Gate:** general rule (User is admin?)

  * `Gate::define('access-admin', fn($user)=>...)`

**Rule:** CRUD/resource permission → Policy
Global/one-off permission → Gate

---

## 18) N+1 prevent: users + posts + comments

N+1 হয় যখন:

* users আনলেন 1 query
* তারপর প্রতি user এর posts আনতে N query
* তারপর প্রতি post এর comments আনতে আরও query

Fix:

* **Eager loading nested**

```php
$users = User::with(['posts.comments'])->paginate(20);
```

* দরকার হলে count:

```php
User::withCount('posts')->with(['posts' => fn($q)=>$q->withCount('comments')])->get();
```

* columns limit:

```php
User::select('id','name')->with(['posts:id,user_id,title', 'posts.comments:id,post_id'])->get();
```

---

এগুলো ১৮টার জন্য আমি আপনার জন্য “short interview answers” ফরম্যাটে ১–২ লাইনের রেডি স্ক্রিপ্টও বানাতে পারি যাতে আপনি কালকে দ্রুত বলতে পারেন।
