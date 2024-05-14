<div align='center'>

# How to use PEST Testing Framework in Laravel
</div>

## Requirement
- PHP 8.1+ or higher installed on your system.

## Install
<b>The first step :</b> is to require Pest as a "dev" dependency in your project by running the following commands on your command line.

```bash
composer require pestphp/pest --dev --with-all-dependencies
```

<b>Secondly : </b>  you'll need to initialize Pest in your current PHP project. This step will create a configuration file named `Pest.php` at the root level of your test suite, which will enable you to fine-tune your test suite later.

```bash
./vendor/bin/pest --init
```

<b>Finally</b>, you can run your tests by executing the pest command.
```bash
./vendor/bin/pest
```

<img src="https://snipboard.io/iMyqrT.jpg">

You can run individually

```bash
./vendor/bin/pest tests/Feature/LoginTest.php
```
## Common Error

#### Error-1 :
When you try to test relevant with your database. First you'll see an error like below - 
<img src="https://snipboard.io/WVtfM9.jpg">

Don't worry just update your `phpunit.xml` file with your database related necessary credentials.

```bash
<?xml version="1.0" encoding="UTF-8"?>
<phpunit xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="https://schema.phpunit.de/10.2/phpunit.xsd" backupGlobals="false" bootstrap="vendor/autoload.php" colors="true" processIsolation="false" stopOnFailure="false" cacheDirectory=".phpunit.cache" backupStaticProperties="false">
  <coverage/>
  <testsuites>
    <testsuite name="Unit">
      <directory suffix="Test.php">./tests/Unit</directory>
    </testsuite>
    <testsuite name="Feature">
      <directory suffix="Test.php">./tests/Feature</directory>
    </testsuite>
  </testsuites>
  <php>
    <server name="APP_ENV" value="testing"/>
    <server name="BCRYPT_ROUNDS" value="4"/>
    <server name="CACHE_DRIVER" value="array"/>
    <server name="DB_CONNECTION" value="mysql"/>
    <server name="DB_DATABASE" value="peoplepro_hrmandcrm"/>
    <server name="MAIL_DRIVER" value="array"/>
    <server name="QUEUE_CONNECTION" value="sync"/>
    <server name="SESSION_DRIVER" value="array"/>
  </php>
  <source>
    <include>
      <directory suffix=".php">./app</directory>
    </include>
  </source>
</phpunit>
```


## Uses

### 1. Login Setup 
You can set login test in your application. First create the File - `/tests/Feature/LoginTest.php` and write the below code.

<b>Test 1 :</b> Get Login Page

```bash
<?php
it('login Page Load', function () {

    $response = $this->get('/login');

    $response->assertStatus(200);
});
```

<b>Test 2 :</b> Login with the credentials

```bash
test('login with username and password', function () {

    $this->post('/login',[
        'username' => 'admin',
        'password' => 'admin',
    ]);

    $this->assertAuthenticated();
});
```

<b>Test 3 :</b> Redirect Dashboard after login.

```bash
it('After login, it will redirect to Admin Dashboard page', function () {
    $this->post('/login',[
        'username' => 'admin',
        'password' => 'admin',
    ]);
    $this->get(url('admin/dashboard'))->assertOk();
});
```

Now run the below command - 

```bash
./vendor/bin/pest tests/Feature/LoginTest.php
```

#### Output : 

<img src="https://snipboard.io/te0vcK.jpg">
