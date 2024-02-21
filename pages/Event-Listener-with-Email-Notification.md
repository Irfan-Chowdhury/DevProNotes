<div align='center'>

# Event-Listener with Email Notification
</div>

According to following my existing project of PeopleProSaaS.

## Setup
Install Laravel and setup other necessary credentials.



### Next Procedure
<b>Step 1 :</b> Create an Event Laravel provides a simple command to generate events. Run the following command in your terminal:
```bash
php artisan make:event CustomerRegistered
```

This will generate an event class named `CustomerRegistered` in the `app/Events` directory. Open this file to see the structure of the event.


<b>Step 2:</b> Create a Listener Next, let’s generate a listener for our event. Run the following command:

```bash
php artisan make:listener NewTenantEmailNotification --event=CustomerRegistered
```
This command will create a listener class named `NewTenantEmailNotification` in the `app/Listeners` directory. Open this file to see the structure of the listener.


<b>Step 3 :</b> Register the Listener To make sure your listener is executed when the event is fired, you need to register it in the EventServiceProvider. Open the EventServiceProvider located in app/Providers and add the following to the listen array:
```php
protected $listen = [
    CustomerRegistered::class => [
        NewTenantEmailNotification::class,
        // You can add another listener
    ],
];
```

<b>Step 4 :</b> Let’s create our first mail :

```bash
php artisan make:mail ConfirmationEmail
```

This command will create a notification class named `ConfirmationEmail` in the `app/Mail` directory. Open this file paste the code.

```php
    <?php

    namespace App\Mail;

    use Illuminate\Bus\Queueable;
    use Illuminate\Contracts\Queue\ShouldQueue;
    use Illuminate\Mail\Mailable;
    use Illuminate\Mail\Mailables\Content;
    use Illuminate\Mail\Mailables\Envelope;
    use Illuminate\Queue\SerializesModels;
    use Illuminate\Mail\Mailables\Address;

    class ConfirmationEmail extends Mailable
    {
        use Queueable, SerializesModels;

        public function __construct(public $request)
        {
            //
        }

        public function envelope(): Envelope
        {
            return new Envelope(
                subject: 'SaaS Confirmation Email',
            );
        }

        public function content(): Content
        {
            return new Content(
                view: 'landlord.public-section.emails.confirmation',
                with: [
                    'name' => $this->request->first_name.' '.$this->request->last_name,
                ],
            );
        }

        public function attachments(): array
        {
            return [];
        }
    }
```

<b>Step 5 :</b> Let’s create our blade file named `confirmatio.blade.php` for mail and paste the code :

```php
    <div>
        Dear {{ $name }},
        <br>

        Your registration for SaaS has been confirmed.

        <br><br>
        Thanks and Regards,
        <br>
        {{-- {{ env('APP_NAME') }} --}}
        {{$generalSetting->footer ?? "no title"}}
    </div>
```


<b>Step 6 :</b> Now put the below code in the handle() method of  `NewTenantEmailNotification` listener :

```php
    public function handle(object $event): void
    {
        // asynchronously
        if (config('mail.is_active'))
            Mail::to($event->customerRequest->email)->send(new ConfirmationEmail($event->customerRequest));
    }
```



<b>Step 7 :</b>  Trigger the Event Now that we have set up our event and listener, it’s time to trigger the event. You can do this from any part of your application where an order is placed. For demonstration purposes, let’s assume it happens in a controller method :

```php
use App\Events\CustomerRegistered;
...

public function customerSignUp(Request $request)
{
    // Other Code 

    // Trigger the event
    event(new CustomerRegistered($request));

}
```

That's It....

## References
- [A Step-by-Step Guide to Laravel Events and Listeners with Examples](https://arjunamrutiya.medium.com/a-step-by-step-guide-to-laravel-events-and-listeners-with-examples-634d7a018fa0)
- [Laravel Notifications: Mail & Database](https://q.agency/blog/laravel-notifications-mail-database/)
- [Laravel](https://laravel.com/)
