<div align='center'>

# Design Pattern
</div>

## 📚 Table of Contents

1. [Singleton design pattern]()
1. [Observer design pattern]()
1. [Factory design pattern]()
1. [Strategy design pattern]()
1. [Repository design pattern]()

<br>



নিচের ৫টা ডিজাইন প্যাটার্ন ইন্টারভিউতে খুব কমন। আমি সহজ বাংলায়, real-life উদাহরণ + ছোট PHP/Laravel-স্টাইল কোড দিয়ে বুঝিয়ে দিচ্ছি। (আমি কোনো কিছু execute করছি না—শুধু ব্যাখ্যা দিচ্ছি।)

---

# ১) Singleton design pattern

**আইডিয়া:** একটা ক্লাসের **শুধু ১টা** অবজেক্ট (instance) পুরো অ্যাপে থাকবে, বারবার নতুন হবে না।

**কখন ব্যবহার করবেন**

* Logger (লগ লেখা)
* Config/Settings
* DB Connection manager (কখনো কখনো)

**কেন দরকার**

* একই জায়গায় একই instance ব্যবহার → consistent + memory বাঁচে

**সহজ উদাহরণ (PHP)**

```php
class Logger {
    private static ?Logger $instance = null;

    // বাইরে থেকে new করা আটকানো
    private function __construct() {}

    public static function getInstance(): Logger {
        if (self::$instance === null) {
            self::$instance = new Logger();
        }
        return self::$instance;
    }

    public function info(string $msg): void {
        echo "[INFO] " . $msg . PHP_EOL;
    }
}

// ব্যবহার
$logger1 = Logger::getInstance();
$logger2 = Logger::getInstance();

$logger1->info("Interview ready!");
// $logger1 এবং $logger2 একই instance
```

**Laravel টিপ:** Laravel এ সাধারণত Service Container দিয়ে `singleton` binding করা হয়, তাই হাতে হাতে singleton কম লিখতে হয়।

---

# ২) Observer pattern

**আইডিয়া:** একটা “Subject” এ কিছু ঘটলে (event), অনেকগুলো “Observer” অটোমেটিক **নোটিফাই** হবে।

**Real-life:** YouTube চ্যানেলে নতুন ভিডিও → সব সাবস্ক্রাইবার নোটিফিকেশন পায়।

**কখন ব্যবহার করবেন**

* Event/Notification system
* Order placed হলে Email/SMS/Stock update
* Laravel Model Observer / Events & Listeners

**সহজ উদাহরণ (PHP)**

```php
interface Observer {
    public function update(string $event): void;
}

class EmailNotifier implements Observer {
    public function update(string $event): void {
        echo "Email sent for: $event\n";
    }
}

class SmsNotifier implements Observer {
    public function update(string $event): void {
        echo "SMS sent for: $event\n";
    }
}

class Subject {
    private array $observers = [];

    public function attach(Observer $observer): void {
        $this->observers[] = $observer;
    }

    public function notify(string $event): void {
        foreach ($this->observers as $observer) {
            $observer->update($event);
        }
    }
}

// ব্যবহার
$order = new Subject();
$order->attach(new EmailNotifier());
$order->attach(new SmsNotifier());

$order->notify("OrderPlaced");
```

**Laravel টিপ:** এটা Laravel এ সবচেয়ে বেশি দেখা যায় **Events/Listeners** বা **Model Observers** হিসেবে।

---

# ৩) Factory pattern

**আইডিয়া:** অবজেক্ট তৈরি করার কাজটা আলাদা একটা “Factory” ক্লাস করবে।
মানে: “কোন ক্লাস বানাবো?” এই সিদ্ধান্ত factory নেবে।

**Real-life:** রেস্টুরেন্টে আপনি “Pizza” বললে কিচেন pizza বানায়, “Burger” বললে burger—আপনি রান্না জানেন না, শুধু অর্ডার দেন।

**কখন ব্যবহার করবেন**

* Payment method: bkash/nagad/card
* Notification channel: email/sms/push
* অনেক subtype থাকলে object creation clean রাখতে

**সহজ উদাহরণ (PHP)**

```php
interface PaymentGateway {
    public function pay(float $amount): string;
}

class BkashPayment implements PaymentGateway {
    public function pay(float $amount): string {
        return "Paid $amount via bKash";
    }
}

class CardPayment implements PaymentGateway {
    public function pay(float $amount): string {
        return "Paid $amount via Card";
    }
}

class PaymentFactory {
    public static function make(string $type): PaymentGateway {
        return match ($type) {
            'bkash' => new BkashPayment(),
            'card'  => new CardPayment(),
            default => throw new Exception("Unknown payment type"),
        };
    }
}

// ব্যবহার
$gateway = PaymentFactory::make('bkash');
echo $gateway->pay(500);
```

---

# 4) Strategy pattern

**আইডিয়া:** একই কাজের (same goal) **একাধিক পদ্ধতি (algorithm)** থাকতে পারে—আর আপনি runtime এ decide করবেন কোনটা ব্যবহার করবেন।

**Real-life:** স্কুলে যাওয়ার strategy: হাঁটা / বাস / রিকশা—গন্তব্য একই, পদ্ধতি আলাদা।

**কখন ব্যবহার করবেন**

* Discount calculation (VIP vs Regular)
* Shipping cost calculation
* Sorting/filtering rules

**সহজ উদাহরণ (PHP)**

```php
interface DiscountStrategy {
    public function apply(float $price): float;
}

class RegularDiscount implements DiscountStrategy {
    public function apply(float $price): float {
        return $price; // no discount
    }
}

class VipDiscount implements DiscountStrategy {
    public function apply(float $price): float {
        return $price * 0.9; // 10% off
    }
}

class Checkout {
    public function __construct(private DiscountStrategy $strategy) {}

    public function total(float $price): float {
        return $this->strategy->apply($price);
    }
}

// ব্যবহার
$checkout1 = new Checkout(new RegularDiscount());
echo $checkout1->total(1000) . "\n";

$checkout2 = new Checkout(new VipDiscount());
echo $checkout2->total(1000) . "\n";
```

---

# 5) Repository pattern

**আইডিয়া:** Database/Storage access করার কোড (query) আলাদা করে Repository তে রাখা।
Controller/Service এ raw query না রেখে clean রাখা।

**কেন দরকার**

* Controller পরিষ্কার হয়
* Testing সহজ হয় (fake repository বসানো যায়)
* DB বদলালেও (MySQL → API/Cache) controller change কম লাগে

**Laravel এ খুব common** (Eloquent Repository)

**সহজ উদাহরণ (Laravel-style)**

```php
// 1) interface
interface UserRepository {
    public function findById(int $id): array;
}

// 2) implementation (ধরা যাক DB/Eloquent দিয়ে আনবেন)
class DbUserRepository implements UserRepository {
    public function findById(int $id): array {
        // এখানে বাস্তবে: User::findOrFail($id)
        return ['id' => $id, 'name' => 'Monjur'];
    }
}

// 3) controller/service depend করবে interface এর উপর
class UserService {
    public function __construct(private UserRepository $users) {}

    public function getUserName(int $id): string {
        $user = $this->users->findById($id);
        return $user['name'];
    }
}

// ব্যবহার
$service = new UserService(new DbUserRepository());
echo $service->getUserName(1);
```

---

## ১ লাইনের ইন্টারভিউ চিটশিট

* **Singleton:** একটা ক্লাসের একটাই instance
* **Observer:** কিছু ঘটলে অনেক listener/observer notify হয়
* **Factory:** কোন object বানাবো—factory decide করে
* **Strategy:** একই কাজের বিভিন্ন algorithm—runtime এ বদলানো যায়
* **Repository:** data access আলাদা layer এ—controller clean, testing easy

আপনি চাইলে আমি এগুলো দিয়ে “১ মিনিটে বলার মতো” ইন্টারভিউ উত্তর স্ক্রিপ্টও বানিয়ে দিতে পারি (প্রতি প্যাটার্ন ১৫–২০ সেকেন্ড)।
