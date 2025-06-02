<div align='center'>

# 🔧 Set Up Laravel Queue Worker and Email Configuration Using Cron Job on cPanel (With Gmail Forwarding)
</div>


## 💡 Common Issue Faced in Shared Hosting Environments 
<!-- আমি মেইল পাঠাতে Mail::to($email)->send() ব্যবহার করছি, কিন্তু এতে ইউজারকে অতিরিক্ত লোড টাইম নিতে হচ্ছে। বিষয়টা সলভ করতে চাই queue() দিয়ে, যেটা লোকালহোস্টে ঠিকভাবে কাজ করে।
শেয়ার হোস্টিং-এ কিভাবে Laravel Mail Queue সিস্টেম ইমপ্লিমেন্ট করবো, যেখানে  queue:work চালানোর সরাসরি অপশন থাকে না?
ইউজার যেন ফর্ম সাবমিট করার সাথে সাথে ফাস্ট রেসপন্স পায়, আর মেইলটা ব্যাকগ্রাউন্ডে পাঠানো হয়। এটা সহজে কিভাবে হেন্ডেল করতে পারি ?

পাশাপাশি  দেখা যায়, Gmail এর ক্রেডেনশিয়াল ইনফু দিয়ে সেটআপ করলে সেগুলা লোকাল মেশিনে কাজ করে কিন্তু Shared Hosting (cPanel) এ কাজ করেনা, error দেখায় । এক্ষেত্রে Shared Hosting কিভাবে মেইলে কনফিগার করা যায় ।  -->

As Laravel developers, we often need to send emails using `Mail::to($email)->send()` or other mechanisms. However, this can significantly slow down the user experience, as the email is sent during the HTTP request. A better approach is to use `queue()` to send emails in the background, allowing users to receive a fast response after form submission.

This setup often works fine in local environments, but implementing **Laravel Mail Queue** on shared hosting (like cPanel) can be challenging due to the lack of direct access to run `php artisan queue:work` continuously.

Additionally, when using Gmail SMTP credentials (e.g., `smtp.gmail.com`, port `587`, encryption `tls`), everything might work perfectly on localhost, but fail on shared hosting with a network or connection error. This is a **common limitation** with shared hosting providers, where external SMTP services like Gmail are often **blocked or restricted**.

---



## ✅ 1. Set Up Laravel Queue Worker Using Cron Job in cPanel

### Step-by-Step:
---
### 1. `.env` file querue connection

open `.env` file and upadte that 

```bash
QUEUE_CONNECTION=database
```

then goto terminal create the jobs migtration file and migrate.
```bash
php artisan queue:table
php artisan migrate

```

### 2. Basic Code Implementation
If you use Laravel Notification,
```php
$admin->notify(new MessageNotification($userInfo));
```

in Notification Class - 

```php
...
use Illuminate\Contracts\Queue\ShouldQueue;

class MessageNotification extends Notification implements ShouldQueue
{
    use Queueable;

    public function __construct()
    {
        //
    }

    public function via(object $notifiable): array
    {
        return ['mail'];
    }

    public function toMail(object $notifiable): MailMessage
    {
        return (new MailMessage)
                    ->line('The introduction to the notification.')
                    ->action('Notification Action', url('/'))
                    ->line('Thank you for using our application!');
    }

    public function toArray(object $notifiable): array
    {
        return [
            //
        ];
    }
}
```

 make sure you `implements` the  `ShouldQueue`

<br>

 ### 3. Queue setup by `Cron Jobs` in cPanel
 
 Goto cPanel and search `Cron Jobs` and then goto that page.

 Suppose I've a cPanel and username `irfandev` and a sub-domain `curtains.irfandev.xyz`. So the project path will be `/home/irfandev/curtains.irfandev.xyz`.

i. If you run the queue in every minutes then select the `Once Per Minute (*****)` from the **Common Settings** dropdown.

ii. Then goto the **Command** input field and paste it and save-

 ```bash
 /usr/local/bin/ea-php74 /home/irfandev/curtains.irfandev.xyz/artisan queue:work --stop-when-empty >> /dev/null 2>&1
 ```
 here `ea-php74` your php version.

 Now run your project and check your mail.

<br>

<img src="https://snipboard.io/36cvO7.jpg" width="600"/>


<br>


## ✅ 2. Setup cPanel Email  in Laravel and Forward to Gmail.

When we try to setup our gmail credentials info in shared hosting like cPanel, this type of issue will be created. 

`Connection could not be established with host "smtp.gmail.com:587": stream_socket_client(): Unable to connect to smtp.gmail.com:587 (Network is unreachable)
`

This error means that your cPanel server is unable to connect to Gmail's SMTP server (smtp.gmail.com:587). The same setup works on your local machine because your local network allows outbound SMTP traffic, but your shared hosting (cPanel) likely blocks it.


So that's why this guide shows how to configure your Laravel project to send emails using your **cPanel email**, and **forward those emails to your Gmail inbox**.

---



### 📌 Part 1: Create an Email Account in cPanel

1. **Login to cPanel.**
2. Go to **Email Accounts**.
3. Click **Create**.

   * **Domain**: Select your domain (e.g., `yourdomain.com`)
   * **Username**: Example `noreply`
   * **Password**: Create a secure password
4. Click **Create**.
5. Once created, click **Connect Devices** beside the email.
6. Note the **SMTP settings**, typically like:

   ```
   SMTP Host: mail.yourdomain.com
   SMTP Port: 465 (SSL) or 587 (TLS)
   Username: noreply@yourdomain.com
   Password: (the one you just set)
   ```
---

<br>

<img src="https://snipboard.io/dDbfMc.jpg" width="600"/>

<br>

<img src="https://snipboard.io/xfiWmQ.jpg" width="600"/>

<br>

<img src="https://snipboard.io/5E1a6W.jpg" width="600"/>

<br>

<img src="https://snipboard.io/pAWDMx.jpg" width="600"/>

<br>

### 📌 Part 2: Configure Laravel to Use cPanel Email

In your Laravel `.env` file, add or update:

```env
MAIL_MAILER=smtp
MAIL_HOST=mail.yourdomain.com
MAIL_PORT=465
MAIL_USERNAME=noreply@yourdomain.com
MAIL_PASSWORD=your_password_here
MAIL_ENCRYPTION=ssl
MAIL_FROM_ADDRESS=noreply@yourdomain.com
MAIL_FROM_NAME="${APP_NAME}"
```

> ⚠️ Replace `yourdomain.com`, username, and password accordingly.

---

### 📌 Part 3: Send a Test Mail

Add a test route in `web.php`:

```php
use Illuminate\Support\Facades\Mail;

Route::get('/test-mail', function () {
    Mail::raw('This is a test email from Laravel using cPanel SMTP.', function ($message) {
        $message->to('yourgmail@gmail.com')->subject('Test Email from Laravel');
    });
    return 'Mail sent!';
});
```

Visit `/test-mail` in your browser and check your Gmail inbox.

---

### 📌 Part 4: Set Up Email Forwarding in cPanel

1. Go back to **cPanel > Forwarders**.
2. Click **Add Forwarder**.
3. Set:

   * **Address to Forward**: e.g., `noreply`
   * **Domain**: your domain
   * **Destination**: your Gmail address
4. Click **Add Forwarder**.

Now, every email sent to `noreply@yourdomain.com` will also be forwarded to your Gmail.


<br>

<img src="https://snipboard.io/HG8qce.jpg" width="600"/>

<br>

<img src="https://snipboard.io/0gstd6.jpg" width="600"/>

<br>

<img src="https://snipboard.io/GtPUaf.jpg" width="600"/>

---

### ✅ Done!

Your Laravel project now uses your cPanel email to send messages, and all emails will be forwarded to your Gmail inbox.

---

### ✅ What You’ll Learn in This Guide

* How to queue emails in Laravel and process them in shared hosting using `Cron Job`
* How to avoid user-facing delays by using queued notifications
* How to configure and send email using cPanel's built-in mail service
* How to **forward emails from your cPanel email to Gmail**

---
