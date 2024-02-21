<div align='center'>

# Event-Listener with Database Notification
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
php artisan make:listener NewTenantDatabaseNotification --event=CustomerRegistered
```
This command will create a listener class named `NewTenantDatabaseNotification` in the `app/Listeners` directory. Open this file to see the structure of the listener.


<b>Step 3 :</b> Register the Listener To make sure your listener is executed when the event is fired, you need to register it in the EventServiceProvider. Open the EventServiceProvider located in app/Providers and add the following to the listen array:
```php
protected $listen = [
    CustomerRegistered::class => [
        NewTenantDatabaseNotification::class,
        // You can add another listener
    ],
];
```


<b>Step 4 :</b> Setup Database notification table by run these commmands -
```bash
php artisan notifications:table
```
And then run migrate

```bash
php artisan migrate
```

<b>Step 5 :</b> Let’s create our first notification :
```bash
php artisan make:notification NewTenantNotify
```

This command will create a notification class named `NewTenantNotify` in the `app/Notifications` directory. Open this file to see the structure of the code.

<b>Step 6 :</b> Now put the below code in the handle() method of  `NewTenantDatabaseNotification` listener :

```php
    use App\Models\User;
    use App\Notifications\NewTenantNotify;
    use Illuminate\Support\Facades\Notification;
    ...

    public function handle(CustomerRegistered $event): void
    {
        $notifiable = User::where('is_super_admin',true)->get();

        Notification::send($notifiable, new NewTenantNotify());
    }
```



<b>Step 7 :</b> Open the `NewTenantNotify.php` file and follow the php code.

```php
<?php

namespace App\Notifications;

use Illuminate\Bus\Queueable;
use Illuminate\Contracts\Queue\ShouldQueue;
use Illuminate\Notifications\Messages\MailMessage;
use Illuminate\Notifications\Notification;

class NewTenantNotify extends Notification
{
    use Queueable;

    public function __construct()
    {
        //
    }

    public function via(object $notifiable): array
    {
        return ['database'];
    }

    public function toMail(object $notifiable): MailMessage
    {
    }


    public function toArray(object $notifiable): array
    {
        return [
			'data'=> "A new client has been registered",
			'link' => route('client.index'),
        ];
    }
}
```

<b>Step 8 :</b>  Trigger the Event Now that we have set up our event and listener, it’s time to trigger the event. You can do this from any part of your application where an order is placed. For demonstration purposes, let’s assume it happens in a controller method :

```php
    use App\Events\CustomerRegistered;
    ...
    
    public function customerSignUp(Request $request)
    {
        // Other Code 

        // Trigger the event
        event(new CustomerRegistered());

    }
```

### Display and Manage the notification

<b>Step 9 :</b> Create a controller like `NotificationController` and paste the below code - 

```php
class NotificationController extends Controller
{
    public function allNotifications()
	{
		$all_notification = auth()->user()->notifications()->get();
		return view('landlord.super-admin.pages.notification.index', compact('all_notification'));
	}

    public function clearAll()
	{
		auth()->user()->notifications()->delete();

		return redirect()->back();
	}

    public function markAsReadNotification()
	{
		auth()->user()->unreadNotifications->markAsRead();
	}
}
```

<b>Step 10 :</b> paste the below code in `web.php` :

```php
    Route::controller(NotificationController::class)->group(function () {
        Route::get('all-notifications', 'allNotifications')->name('seeAllNotification');
        Route::get('clearAll', 'clearAll')->name('clearAllNotification');
        Route::get('markAsRead', 'markAsReadNotification')->name('markAsReadNotification');
    });
```

<b>Step 11 :</b> paste the below code in in your `header.blade.php` file :

```php
    <li class="nav-item">
        <a rel="nofollow" id="notify-btn" href="#" class="nav-link dropdown-item" data-toggle="tooltip"
            title="{{__('Notifications')}}">
            <i class="dripicons-bell"></i>
            @if(auth()->user()->unreadNotifications->count())
                <span class="badge badge-danger">
                    {{auth()->user()->unreadNotifications->count()}}
                </span>
            @endif
        </a>
        <ul class="right-sidebar">
            <li class="header">
                <span class="pull-right"><a href="{{route('clearAllNotification')}}">{{__('Clear All')}}</a></span>
                <span class="pull-left"><a href="{{route('seeAllNotification')}}">{{__('See All')}}</a></span>
            </li>
            @foreach(auth()->user()->notifications as $notification)
                <li><a class="unread-notification"
                        href={{$notification->data['link']}}>{{$notification->data['data']}}</a></li>
            @endforeach
        </ul>
    </li>
```

and add the scripts in `header.blade.php` file -

```php
@push('scripts')
<script type="text/javascript">
    (function ($) {

        "use strict";

        $('#notify-btn').on('click', function (event) {
            event.preventDefault();
            $('.badge.badge-danger').empty();
            $.ajax({
                url: '{{route('markAsReadNotification')}}',
                dataType: "json",
                success: function (result) {
                },
            });
        })

    })(jQuery);
</script>

@endpush
```

The visible data show like that -

<b>Screenshot 1 :</b> 
<br>
<img src="https://snipboard.io/5Im1bn.jpg">

<b>Screenshot 2 :</b>  
<br>
<img src="https://snipboard.io/NIKOvy.jpg">

<b>Step 12 :</b> create a blade file like `index.blade.php` and paste below the code to see all data  :

```php
	<section>
		<div class="container">
			<div class="card">
                <div class="card-header text-center">
                    <h2>All Notifications</h2>
                </div>
				<div class="card-body">
                    @foreach($all_notification as $notification)
                        <div class="appointment-list-item">
                        <a href={{$notification->data['link']}}>{{$notification->data['data']}}</a>
                        </div>
                    @endforeach

					@if(count($all_notification) > 0)
						<div class="text-center">
							<a href="{{route('clearAllNotification')}}" class="btn btn-link">{{__('Clear All')}}</a>
						</div>
					@else
						<p class="large-text dark-text text-center">{{__('No notifications for you at the moment!')}}</p>
					@endif
				</div>
			</div>
		</div>
	</section>
```

<b>Screenshot 3 :</b>  
<br>
<img src="https://snipboard.io/nvpAhQ.jpg">

That's It....

## References
- [A Step-by-Step Guide to Laravel Events and Listeners with Examples](https://arjunamrutiya.medium.com/a-step-by-step-guide-to-laravel-events-and-listeners-with-examples-634d7a018fa0)
- [Laravel Notifications: Mail & Database](https://q.agency/blog/laravel-notifications-mail-database/)
- [Laravel](https://laravel.com/)
