<div align='center'>

# Autoloading and Dependency Management
</div>

<br><br>

# 1. Introduction to Composer

### Regular Issue: 
i. বার বার require, include করা পসিবল না । <br>
ii. File path & Directory path নিয়ে ইশু <br>
এগুলার সল্যুশন Autoload.

### Benifit of using Composer :

1. Save time of Developers

1. <b>Dependency Management:</b> Composer automatically handles package dependencies, ensuring you have all necessary libraries with compatible versions for your project.

1. <b>Autoloading:</b> Composer provides an autoloader, so you don't need to manually include or require each PHP file, making your code cleaner and more maintainable.

1. <b>Version Control:</b> Composer locks package versions, ensuring consistency across different environments. This prevents version conflicts and makes deployments smoother.

1. <b>Reusable Packages:</b> Composer enables developers to use and share reusable PHP packages from Packagist (the default package repository), reducing development time and effort.

1. <b>Community Contributions:</b> Composer fosters a large ecosystem of open-source libraries, letting you integrate high-quality, community-maintained solutions quickly.

### How to install package.
Create a file composer.json and write the line

```json
"require": {
    "php": ">= 8.0",
    "laravel/framework": ">= 9.0"
},
```

#### Commands :

1. now install command 

```bash
composer install
```

A vendor folder will be created. In a `index.php` file we can declare - 

```php
require_once "vendor/autoload.php"
```

#### Commands :

2. If new file added or `autoload.php` file not found just write the command - 

```bash
composer dump-autoload
```

# 2. Autoloading in PHP

Without using composer, if any file need to add automatice follow the `spl_autoload_register()` - built in function.

```php
// using an anonymous function

spl_autoload_register(function ($className) {
    
    $baseDir = "app/classes";

    require_once $baseDir.$className. '.php';
});
```

# 3. Autoloading using Composer

`PSR-4 ` : If you autoload the class, you've to use namespace.

`composer.json` - 

```json
"autoload": {
    "psr-4": {
        "App\\": "app/",
        "Database\\Factories\\": "database/factories/",
        "Database\\Seeders\\": "database/seeders/"
    }
},
```

<b>Example :</b> in `index.php` you can write the code

```php
use App\Classess\Bike;

require "vendor/autoload.php";

$bike = new Bike();
echo $bike->methodName();
```

# 4. Autoloading files using Composer

```json
"autoload": {
    "psr-4": {

    },
    "files" : ["helpers/helper.php"]
},
```

let any method name `calculate()` in helper class, then we just need to write only the `calculate()` method name.

```php
use App\Classess\Bike;

require "vendor/autoload.php";

$bike = new Bike();
echo $bike->methodName();

calculate();
```

# 4. Managing dependency with composer

<h3>Issue :</h3>  Without using any Package Management,

- Using a pacakge manually added using `include`,
- If need to update
- If need to remove, all can do manually.

but all are time consuming, that's why need to use composer. 


#### Commands :

3. If package install - 

```bash
composer require irfan-chowdhury/version-elevate
```
or
```bash
composer require irfan-chowdhury/version-elevate:1.23.0
```

4. For update the latest all package, <br>
or downgrade the any version of package, just goto `composer.json` file and update the version number. 
```bash
composer update
```


5. remove any package - 

```bash
composer remove irfan-chowdhury/version-elevate
```


6. Display all packages - 

```bash
composer show
```

7. Search package from online in terminal - 

```bash
composer search faker
```
Some pacakge list will show in your terminal relevant with the facker.

To know more about composer, Please visit : https://devsonket.com/composer/


# 5. Advanced Dependency Management

#### `composer.lock` 
- It will be created when you use `composer install`.
- Always add in Github in your every repository.
- All packages details of your project, will be stored in that `composer.lock` file.
- When other developers work a project, the info all of packages should be same. Otherwise sometimes may face problem during install or other version related issue.

#### `required-dev`

#### Commands :

8. If you install package with require dev - 

```bash
composer require pestphp/pest --dev
```

```json
"require-dev": {
    "pestphp/pest": "^3.5",
},
```

9. If you want to ignore dev.
```bash
composer install --no-dev
```
All pacakges will be installed except the `require-dev` parts.

10. To check all commands.
```bash
composer 
```

11. For help -
```bash
composer help
```

12. Official Docs <br>
`Official Docs --> Documentation --> Book --> Command Line interface/Commands`

or visit : https://getcomposer.org/doc/03-cli.md







