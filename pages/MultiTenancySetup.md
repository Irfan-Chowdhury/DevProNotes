<div align='center'>

# Multi Tenancy Setup in Laravel App
</div>

## What is multi-tenancy ? 
Multi-tenancy is a software architecture and design approach that allows a single software application to serve multiple, separate, and independent clients, known as "tenants." Each tenant typically operates in isolation from one another, with their own data, configurations, and user accounts, despite using the same underlying software instance. This approach is commonly used in various types of software, including web applications, databases, and cloud services. This is the ability to provide your service to multiple users (tenants) from a single hosted instance of the application. This is contrasted with deploying the application separately for each user. 

## Virtual Host Setup
Before setup the SaaS in your project, please setup the virtual host first.

- For linux machine, please follow this article : [Linux Virtualhost Setup](https://github.com/Irfan-Chowdhury/DevProTips/blob/main/pages/virtualhost.md)

- For windows, there are so many resources on youtube, google. Please check.

## Package Installation
First, require the package using composer:
```bash
composer require stancl/tenancy
```

Then, run the tenancy:install command:
```bash
php artisan tenancy:install
```

Let's run the migrations:
```bash
php artisan migrate
```

Register the service provider in `config/app`.php. Make sure it's on the same position as in the code snippet below:
```php
/*
 * Application Service Providers...
 */
 ...
App\Providers\TenancyServiceProvider::class, 
```

## Creating a tenant model
Now you need to create a Tenant model. Create the file using `php artisan make:model Tenant`.

```php
<?php

namespace App\Models;

use Stancl\Tenancy\Database\Models\Tenant as BaseTenant;
use Stancl\Tenancy\Contracts\TenantWithDatabase;
use Stancl\Tenancy\Database\Concerns\HasDatabase;
use Stancl\Tenancy\Database\Concerns\HasDomains;

class Tenant extends BaseTenant implements TenantWithDatabase
{
    use HasDatabase, HasDomains;
}
```
Please note: if you have the models anywhere else, you should adjust the code and commands of this tutorial accordingly.


But if want to customize the tenant table then you can follow this - 
<img src="https://snipboard.io/WvbRyY.jpg">


## PeopleProSAAS - Setup Guideline

### (.env) file setup
I was added and modified the environment variable.
```bash
CENTRAL_DOMAIN=peopleprosaas.test
CPANEL_API_KEY=
CPANEL_USER_NAME=

DB_PREFIX=
DB_CONNECTION=peopleprosaas_landlord
DB_HOST=localhost
DB_PORT=3306
DB_DATABASE=
DB_USERNAME=root
DB_PASSWORD=irfan95

LANDLORD_DB=peoplepro_landlord
```
API_KEY, USER_NAME, PREFIX and othres modification will be applicable during deploy on the cPanel Server.

### config/database.php
Goto `config/database.php` then create two more connections like <b>mysql</b>.

1. One is for Landlord
```php
'peopleprosaas_landlord' => [
    'driver' => 'mysql',
    'url' => env('DATABASE_URL'),
    'host' => env('DB_HOST', '127.0.0.1'),
    'port' => env('DB_PORT', '3306'),
    'database' => env('LANDLORD_DB', 'forge'),
    'username' => env('DB_USERNAME', 'forge'),
    'password' => env('DB_PASSWORD', ''),
    'unix_socket' => env('DB_SOCKET', ''),
    'charset' => 'utf8mb4',
    'collation' => 'utf8mb4_unicode_ci',
    'prefix' => '',
    'prefix_indexes' => true,
    'strict' => false,
    'engine' => null,
    'options' => extension_loaded('pdo_mysql') ? array_filter([
        PDO::MYSQL_ATTR_SSL_CA => env('MYSQL_ATTR_SSL_CA'),
    ]) : [],
],
```

2. Another is for tenant.
```php
'peopleprosaas_tenant' => [
    'driver' => 'mysql',
    'url' => env('DATABASE_URL'),
    'host' => env('DB_HOST', '127.0.0.1'),
    'port' => env('DB_PORT', '3306'),
    'database' => env('DB_DATABASE', 'forge'),
    'username' => env('DB_USERNAME', 'forge'),
    'password' => env('DB_PASSWORD', ''),
    'unix_socket' => env('DB_SOCKET', ''),
    'charset' => 'utf8mb4',
    'collation' => 'utf8mb4_unicode_ci',
    'prefix' => '',
    'prefix_indexes' => true,
    'strict' => false,
    'engine' => null,
    'options' => extension_loaded('pdo_mysql') ? array_filter([
        PDO::MYSQL_ATTR_SSL_CA => env('MYSQL_ATTR_SSL_CA'),
    ]) : [],
],
```

### config/tenancy.php
Now we need to tell the package to use this custom model. Open the `config/tenancy.php` file and modify the line below:

<img src="https://snipboard.io/5lPwk3.jpg">

Please look the `#Modified` word. I have to update these line.


### Kernel.php
Goto `app/Http/Kernel.php` and then add `universel` array in `middlewareGroups` 

```php
protected $middlewareGroups = [
    'web' => [
        ...
    ],

    'api' => [
        ...
    ],
    'universal' => [], // <---This line
];
```

### TenancyServiceProvider

Goto `app/Provider/TenancyServiceProvider.php`. In the initial stage you will see the `Jobs\SeedDatabase::class` in comment. If you want to use Seeder then comment out.


then update the `mapRoutes()` method.
```php
protected function mapRoutes()
{
    if (file_exists(base_path('routes/tenant.php'))) {
        Route::namespace(static::$controllerNamespace)
            ->group(base_path('routes/tenant.php'));
    }
}
```

### RouteServiceProvider
Goto `app/Provider/RouteServiceProvider.php` and then configure your code like below - 

```php
public function boot()
{
    $this->mapApiRoutes();
    $this->mapWebRoutes();
}

protected function centralDomains(): array
{
    return config('tenancy.central_domains', []);
}

protected function mapWebRoutes()
{
    foreach ($this->centralDomains() as $domain) {
        Route::middleware('web')
            ->domain($domain)
            ->group(base_path('routes/web.php'));

        Route::middleware('web')
            ->domain($domain)
            ->group(base_path('routes/general.php'));
    }
}

protected function mapApiRoutes()
{
    foreach ($this->centralDomains() as $domain) {
        Route::prefix('api')
            ->domain($domain)
            ->middleware('api')
            ->group(base_path('routes/api.php'));
    }
}
```

### ViewComposerServiceProvider

This is my another custom service provider. The GeneralSeting exists in both landlord and tenant. So need identify the host first and then fetch the actual data and share with anothers necessary files. Otherwise it'll give errors.

```php
public function boot(): void
{
    if (Schema::hasTable('general_settings') && in_array(request()->getHost(), config('tenancy.central_domains'))) {
        $generalSetting = GeneralSetting::latest()->first();
        view()->composer([
            'landlord.public-section.layouts.master',
            'landlord.public-section.pages.landing-page.index',
        ], function ($view) use ($generalSetting) {
            $view->with('generalSetting', $generalSetting);
        });
    }
}
```

### routes/tenant.php
During install the package, a route file name `routes/tenant.php` will be created automatically. Just move your `web.php` file code to `tenant.php`. But before use this codes (already some codes will exists) and paste your code in group block. 

```php
declare(strict_types=1);

use Illuminate\Support\Facades\Route;
use Stancl\Tenancy\Middleware\InitializeTenancyByDomain;
use Stancl\Tenancy\Middleware\PreventAccessFromCentralDomains;


Route::middleware(['XSS', 'web',InitializeTenancyByDomain::class, PreventAccessFromCentralDomains::class])->group(function () {
    
    // Your existing route code
    ...
});
```

### main.blade.php (Tenant)
Goto `resources/views/layout/main.blade.php`. Here your all existing includes file path have to be changed. Just add `../../` before your original path. Example :

```php
# Normal Image File
<link rel="icon" type="image/png" href="{{asset('../../images/logo/'.$general_settings->site_logo)}}"/>


# CSS File
<link rel="preload" as="style" onload="this.onload=null;this.rel='stylesheet'" href="{{ asset('../../vendor/bootstrap/css/bootstrap.min.css') }}">

# Script File
<script type="text/javascript" src="{{ asset('../../vendor/datatable/datatable.responsive.boostrap.min.js') }}"></script>
```

By the you don't worry about Landlord part. It will work as usual a Laravel app work.

## Usages
In any controller just use this piece of codes.

```php
public function create()
{
    //creating tenant
    $tenant = Tenant::create(['id' => $request->tenant]);
    $tenant->domains()->create(['domain' => $request->tenant.'.'.env('CENTRAL_DOMAIN')]); // This Line

    $tenant->run(function ($tenant) use ($request) { 
        
        // your code 
        // Here if you pass any default data to tenant related tables;
    });
}
```

## Some General Commands
- To check all tenants list 
    ```bash
    php artisan tenants:list
    ```

### Tenant migrate from central 
- You can run tenant migrations using the command : 
    ```bash
    php artisan tenants:migrate
    ```

- You may specify the tenant(s) using the --tenants option.
    ```bash
    php artisan tenants:migrate --tenants=foo 
    ```

- If you have others directory, you have to mention with path also :
    ```bash  
    php artisan tenants:migrate --path=database/migrations/another_directory
    ```


<i>Note: Tenant migrations must be located base on your desired path which you mentioned it in "config/tenancy.php".</i>


- You can run migrations from outside the command line as well. To run migrations for a tenant in your code, use Artisan::call():

    ```php
    $tenant = Tenant::create('foo');

    Artisan::call('tenants:migrate', [
        '--tenants' => [$tenant->id]
    ]);
    ```
 - Reference : https://tenancyforlaravel.com/docs/v2/tenant-migrations/

#### <i>Done !! Now run your app in your local machine</i>

## Credits
- Reference : [Tenancy for Laravel](https://tenancyforlaravel.com/) ||  [Adding multi tenancy to an existing Laravel web application](https://www.youtube.com/watch?v=BitZhTeLgR4)
- Guided by : [Ashfaqur Rahman](https://github.com/ashfaqdev)