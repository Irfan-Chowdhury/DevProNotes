<div align='center'>

# Table of Contents
</div>



- [1. Storage link not working on hosting cPanel](#1-storage-link-not-working-on-hosting-cpanel)
- [2. Set Up Laravel Queue Worker Using Cron Job in cPanel](#-2-set-up-laravel-queue-worker-using-cron-job-in-cpanel)
- [3. Queue setup by `Cron Jobs` in cPanel](#-3-queue-setup-by-cron-jobs-in-cpanel)
- [4. Setup cPanel Email  in Laravel and Forward to Gmail.](#-4-setup-cpanel-email--in-laravel-and-forward-to-gmail)


<br>

# ✅ 1. Storage link not working on hosting cPanel

### Problem Statement : 
I've created a storage link with php artisan storage:link and it's working totally fine on localhost, However, when I deploy my project on a shared hosting cPanel, it does not render any images. 

Solutions : 
- Delete the storage link folder created on your local host from your c-panel
-  Create a route to run you php artisan storage:link command as below :

    ```php
    use Illuminate\Support\Facades\Artisan;

    Route::get('/storage_link', function (){ 
        Artisan::call('storage:link'); 
        return 'Success !';
    });
    ```
- On your bowser got to the route /storage_link,.. this will create a new system link to you storage file.

- Your `APP_URL` on `.env` file should be 

    ```bash
    APP_URL=your_site_url
    ```
- Check the `config/filesystems.php`

    ```php
        'public' => [
            'driver' => 'local',
            'root' => storage_path('app/public'),
            'url' => env('APP_URL').'/storage',
            'visibility' => 'public',
        ],
    ```

- Recommended to fetch the image like this - 
    ```php
    isset($path) && (Storage::disk('public')->exists($path)) ? Storage::url($path) : "https://dummyimage.com/50x50/000000/0f6954.png&text=$default";
    ```

<br>

# ✅ 2. Set Up Laravel Queue Worker Using Cron Job in cPanel

### Problem Statement : 
আমি মেইল পাঠাতে Mail::to($email)->send() ব্যবহার করছি, কিন্তু এতে ইউজারকে অতিরিক্ত লোড টাইম নিতে হচ্ছে। বিষয়টা সলভ করতে চাই queue() দিয়ে, যেটা লোকালহোস্টে ঠিকভাবে কাজ করে।
শেয়ার হোস্টিং-এ কিভাবে Laravel Mail Queue সিস্টেম ইমপ্লিমেন্ট করবো, যেখানে  queue:work চালানোর সরাসরি অপশন থাকে না?
ইউজার যেন ফর্ম সাবমিট করার সাথে সাথে ফাস্ট রেসপন্স পায়, আর মেইলটা ব্যাকগ্রাউন্ডে পাঠানো হয়। এটা সহজে কিভাবে হেন্ডেল করতে পারি ?


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

 # ✅ 3. Queue setup by `Cron Jobs` in cPanel
 
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


# ✅ 4. Setup cPanel Email  in Laravel and Forward to Gmail.

### Problem Statement : 
`Connection could not be established with host "smtp.gmail.com:587": stream_socket_client(): Unable to connect to smtp.gmail.com:587 (Network is unreachable)
`

This error means that your cPanel server is unable to connect to Gmail's SMTP server (smtp.gmail.com:587). The same setup works on your local machine because your local network allows outbound SMTP traffic, but your shared hosting (cPanel) likely blocks it.

---
This guide shows how to configure your Laravel project to send emails using your **cPanel email**, and **forward those emails to your Gmail inbox**.

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

<img src="https://snipboard.io/ioldCL.jpg" width="600"/>

<br>

<img src="https://snipboard.io/xfiWmQ.jpg" width="600"/>

<br>

<img src="https://snipboard.io/owsCqv.jpg" width="600"/>

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

<img src="https://snipboard.io/xWiKNR.jpg" width="600"/>

<br>

<img src="https://snipboard.io/0gstd6.jpg" width="600"/>

<br>

<img src="https://snipboard.io/YUXl8B.jpg" width="600"/>


---

### ✅ Done!

Your Laravel project now uses your cPanel email to send messages, and all emails will be forwarded to your Gmail inbox.

---
