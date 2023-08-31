<div align='center'>

# Multi Tenancy Setup in Laravel App
</div>

## What is multi-tenancy ? 
Multi-tenancy is a software architecture and design approach that allows a single software application to serve multiple, separate, and independent clients, known as "tenants." Each tenant typically operates in isolation from one another, with their own data, configurations, and user accounts, despite using the same underlying software instance. This approach is commonly used in various types of software, including web applications, databases, and cloud services. This is the ability to provide your service to multiple users (tenants) from a single hosted instance of the application. This is contrasted with deploying the application separately for each user. 

## Installation
First, require the package using composer:
```
composer require stancl/tenancy
```

Then, run the tenancy:install command:
```
php artisan tenancy:install
```

Let's run the migrations:
```
php artisan migrate
```

Register the service provider in `config/app`.php. Make sure it's on the same position as in the code snippet below:
```
/*
 * Application Service Providers...
 */
 ...
App\Providers\TenancyServiceProvider::class, 
```

## Creating a tenant model
Now you need to create a Tenant model. Create the file `app/Models/Tenant.php`.

```
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

## PeopleProSAAS - Setup Guideline

### config/tenancy.php
Now we need to tell the package to use this custom model. Open the `config/tenancy.php` file and modify the line below:


<img src="https://snipboard.io/fdvNzs.jpg">

Please look the `#Modified` word. I have to update these line.

### (.env) file setup
I was added and modified the environment variable.
```
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

### config/database.php
Goto `config/database.php` then create two more connections like <b>mysql</b>.

1. One is for Landlord
```
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
```
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

### TenancyServiceProvider

Goto `app/Provider/TenancyServiceProvider.php`. In the initial stage you will see the `Jobs\SeedDatabase::class` in comment. If you want to use Seeder then comment out.


then update the `mapRoutes()` method.
```
protected function mapRoutes()
{
    if (file_exists(base_path('routes/tenant.php'))) {
        Route::namespace(static::$controllerNamespace)
            ->group(base_path('routes/tenant.php'));
    }
}
```

### Kernel.php
Goto `app/Http/Kernel.php` and then add `universel` array in `middlewareGroups` 

```
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

### RouteServiceProvider
Goto `app/Provider/RouteServiceProvider.php` and then configure your code like below - 

```
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

```
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
Just put the code before your existing code .

```
Route::middleware(['XSS', 'web',InitializeTenancyByDomain::class, PreventAccessFromCentralDomains::class])->group(function () {
    
    // Your existing route code
    ...
});
```

### main.blade.php (Tenant)
Goto `resources/views/layout/main.blade.php`. Here your all existing includes file path have to be changed. Just add `../../` before your original path. Example :

```
# Normal Image File
<link rel="icon" type="image/png" href="{{asset('../../images/logo/'.$general_settings->site_logo)}}"/>


# CSS File
<link rel="preload" as="style" onload="this.onload=null;this.rel='stylesheet'" href="{{ asset('../../vendor/bootstrap/css/bootstrap.min.css') }}">

# Script File
<script type="text/javascript" src="{{ asset('../../vendor/datatable/datatable.responsive.boostrap.min.js') }}"></script>
```

Credits
- Guided by [Ashfaqur Rahman](https://github.com/ashfaqdev)