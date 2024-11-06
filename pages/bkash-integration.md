<div align='center'>

# bKash Payment Gatway Integration in Laravel
</div>

Then are some types of bKash Integration. Here we used `Tokenized solution`.

## Step-1 : Registration
First of all you need a marchant account and then need to register your website there.

- Visit Website :  https://pgw-integration.bkash.com


<img src="https://snipboard.io/N7BqGZ.jpg">


- Setup Account Info

<img src="https://snipboard.io/fwN42A.jpg">


- Product Request

<img src="https://snipboard.io/2gfH5L.jpg">

- Product List

<img src="https://snipboard.io/6TOp1h.jpg">

- Overview

<img src="https://snipboard.io/39zEhD.jpg">


## Step-2 : Sandbox Validation
First of all follow the developer documentation.


Visit the link : https://developer.bka.sh/docs/tokenized-checkout-overview


Our Sandbox Credentials will be look like that - 
<img src="https://snipboard.io/lRGLNS.jpg">



### 1. [Grand Token ](https://developer.bka.sh/docs/grant-token-1)

Request URL: `{base_URL}/tokenized/checkout/token/grant`
Here the base_URL will be - `https://tokenized.sandbox.bka.sh/v1.2.0-beta/`

Now follow the screenshot given below -

<img src="https://snipboard.io/yhFaTi.jpg">

in POSTMAN - 

Headers
<img src="https://snipboard.io/vymjuI.jpg">

Body
<img src="https://snipboard.io/Mm32FI.jpg">

Response Result - 

<img src="https://snipboard.io/XAGOzV.jpg">

### 2. [Create Payment](https://developer.bka.sh/docs/create-payment-2)

Follow the format -

```bash
POST /tokenized/checkout/create HTTP/1.1
Host: {base_URL}
Content-Type: application/json
Accept: application/json
authorization: id_token
x-app-key: x-app-key

{  
   "mode": "0011",
   "payerReference": "01723888888",
   "callbackURL": "yourDomain.com",
   "merchantAssociationInfo": "MI05MID54RF09123456One"
   "amount": "500",
   "currency": "BDT",
   "intent": "sale",
   "merchantInvoiceNumber": "Inv0124"
}
```

in Postman - 

Header -
<img src="https://snipboard.io/lUSMzX.jpg">

Body - 
<img src="https://snipboard.io/1CYhKN.jpg">

Response
<img src="https://snipboard.io/vOhsuy.jpg">


### 3. [Execute Payment](https://developer.bka.sh/docs/execute-payment-2)


First copy the `bKashURL` and then goto the link and make payment from their site first -  

For an example, sample link look like- 

```bash
https://sandbox.payment.bkash.com/?paymentId=TR0011hEN7KTZ1718449546941&hash=)gqMffGT.r.4*dLWGcc)mE_6q9U)wmmh9SI6hTlkjzNc!IFGOZZCN5Fe1I0FGRtIXxl!sNdP00LAv)mjDLg6iu8cAKr**0g(WHZC1718449546941&mode=0011&apiVersion=v1.2.0-beta/
```

<img src="https://snipboard.io/EKVyDB.jpg">

<img src="https://snipboard.io/GuQt13.jpg">

<img src="https://snipboard.io/zKxSnM.jpg">

<img src="https://snipboard.io/toBdAw.jpg">


<br>

After creating the payment, now goto postman and follow the format -

```bash
POST /tokenized/checkout/execute HTTP/1.1
Host: {base_URL}
Accept: application/json
authorization: id_token
x-app-key: x-app-key

{
	"paymentID" : "TR0011ON1565154754797"
}
```


in Postman - 

Header -
<img src="https://snipboard.io/CqiEw8.jpg">

Body - 
<img src="https://snipboard.io/r30Zwv.jpg">

Response
<img src="https://snipboard.io/v7feu0.jpg">


### 4. Verify Sandbox Validation

Create Payment Sandbox Test

<img src="https://snipboard.io/uvwAdr.jpg">


Execute Payment Sandbox Test

<img src="https://snipboard.io/3BHItK.jpg">

Success Output

<img src="https://snipboard.io/07Rre1.jpg">


### 5. Live Credentials

After doing all these, finally you will get the Live Credentials. 

<img src="https://snipboard.io/XnYxW4.jpg">


## Step-3 : Implement the Code

### #1 `.ENV`

Put the value in .env file -

```bash
# Sandbox Credentials
APP_URL=your_root_domain
BKASH_TOKENIZE_SANDBOX=true
BKASH_TOKENIZE_BASE_URL=https://tokenized.sandbox.bka.sh/v1.2.0-beta/tokenized
BKASH_TOKENIZE_VERSION="v1.2.0-beta"
BKASH_TOKENIZE_APP_KEY=your_sandbox_app_key
BKASH_TOKENIZE_APP_SECRET=your_sandbox_app_secret
BKASH_TOKENIZE_USER_NAME=01XXXXXXXXX
BKASH_TOKENIZE_PASSWORD=your_sandbox_app_password


# Live Credentials
# APP_URL=your_root_domain
# BKASH_TOKENIZE_SANDBOX=false
# BKASH_TOKENIZE_BASE_URL=https://tokenized.pay.bka.sh/v1.2.0-beta/tokenized
# BKASH_TOKENIZE_VERSION="v1.2.0-beta"
# BKASH_TOKENIZE_APP_KEY=your_live_app_key
# BKASH_TOKENIZE_APP_SECRET=your_live_app_secret
# BKASH_TOKENIZE_USER_NAME=01XXXXXXXXX
# BKASH_TOKENIZE_PASSWORD=your_live_app_password
```

### #2 `config/bkash.php`
Please create the file `config/bkash.php` and paste the code given below - 

```php
<?php

return [
    "bkash_version" => env("BKASH_TOKENIZE_VERSION", ""),
    "bkash_sandbox" => env("BKASH_TOKENIZE_SANDBOX", true),
    "bkash_base_url" => env("BKASH_TOKENIZE_BASE_URL", ""),
    "bkash_app_key" => env("BKASH_TOKENIZE_APP_KEY", ""),
    "bkash_app_secret" => env("BKASH_TOKENIZE_APP_SECRET", ""),
    "bkash_username" => env("BKASH_TOKENIZE_USER_NAME", ""),
    "bkash_password"  => env("BKASH_TOKENIZE_PASSWORD", ""),
    // "bkash_callback_url" => env('APP_URL'). '/bkash/after-create-payment',
    "bkash_callback_url"  => url('/bkash/callback'),
    'bkash_timezone' => 'Asia/Dhaka',
];
```

<b>Note : </b> Please set your root domain in APP_URL in .env file

### #3 `web.php`
Please open your `routes/web.php` file and use the code

```php
use App\Http\Controllers\PaymentController;

Route::controller(PaymentController::class)->group(function () {
    Route::get('checkout', 'checkout')->name('checkout');
    Route::post('payment/process', 'paymentProcees')->name('payment.process');
    Route::post('payment/{payment_method}/pay', 'paymentPayPage')->name('payment.pay.page');
    Route::post('payment/{payment_method}/pay/confirm', 'paymentPayConfirm')->name('payment.pay.confirm');
    Route::post('payment/{payment_method}/pay/cancel', 'paymentPayCancel')->name('payment.pay.cancel');
    //bkash
    Route::get('/bkash/callback','bkashCallback');
    Route::get('payment-success', 'paymentSuccess')->name('payment.success');
});
```

### 4. PaybleContract
create an interface `app\Contracts\PaybleContract.php` and paste the code given below - 

```php
<?php

namespace App\Contracts\Payble;

interface PaybleContract
{
    public function pay($request, $otherRequest);
    public function cancel();
}
```

### 5. BkashPayment class

This is the main part for bKash. Create a Payment Class `app\Payment\BkashPayment.php` which implements the interface. Now use the code.

```php
<?php
declare(strict_types=1);

namespace App\Payment;

use App\Contracts\Payble\PaybleContract;
use Exception;
use Illuminate\Http\Request;
use Illuminate\Support\Facades\Session;

class BkashPayment implements PaybleContract
{
    public $errorCodes = [
        2001, 2002, 2003, 2004, 2005, 2006, 2007, 2008, 2009, 2010,
        2011, 2012, 2013, 2014, 2015, 2016, 2017, 2018, 2019, 2020,
        2021, 2022, 2023, 2024, 2025, 2026, 2027, 2028, 2029, 2030,
        2031, 2032, 2033, 2034, 2035, 2036, 2037, 2038, 2039, 2040,
        2041, 2042, 2043, 2044, 2045, 2046, 2047, 2048, 2049, 2050,
        2051, 2052, 2053, 2054, 2055, 2056, 2057, 2058, 2059, 2060,
        2061, 2062, 2063, 2064, 2065, 2066, 2067, 2068, 2069,
        9999, 503,
    ];

    private $base_url;
    private $app_key;
    private $app_secret;
    private $username;
    private $password;
    private $callbackURL;


    public function __construct()
    {
        $this->base_url = config('bkash.bkash_base_url');
        $this->app_key = config('bkash.bkash_app_key');
        $this->app_secret = config('bkash.bkash_app_secret');
        $this->username = config('bkash.bkash_username');
        $this->password = config('bkash.bkash_password');
        $this->callbackURL = config('bkash.bkash_callback_url');
    }


    public function pay($request, $otherRequest)
    {
        $grantTokenData = $this->grantToken();

        if(!isset($grantTokenData['id_token']) && in_array($grantTokenData['statusCode'], $this->errorCodes))
        {
            $statusCode = $grantTokenData['statusCode'];
            $statusMessage = $grantTokenData['statusMessage'];
            session()->flash('message',"$statusCode | $statusMessage ");
            return redirect(route("payment.pay.page",'bkash'), 307);
        }

        Session::put('id_token', json_encode($grantTokenData['id_token']));

        $createPaymentObjectData = $this->createPayment((float)$request->price, $grantTokenData['id_token']);

        if(isset($createPaymentObjectData->statusCode) && in_array($createPaymentObjectData->statusCode, $this->errorCodes)) {
            $statusCode = $createPaymentObjectData->statusCode;
            $statusMessage = $createPaymentObjectData->statusMessage;
            session()->flash('message',"$statusCode | $statusMessage ");
            return redirect(route("payment.pay.page",'bkash'), 307);
        }

        return redirect()->away($createPaymentObjectData->{'bkashURL'});
    }


    private function grantToken() : array
    {
        $_SESSION['id_token'] = null;
        $post_token = array(
            'app_key'=> $this->app_key,
            'app_secret'=> $this->app_secret
        );

        $url = curl_init("$this->base_url/checkout/token/grant");

        $request_data_json=json_encode($post_token);
        $header = array(
            'Content-Type: application/json',
            "username:$this->username",
            "password:$this->password"
        );

        curl_setopt($url,CURLOPT_HTTPHEADER, $header);
        curl_setopt($url,CURLOPT_CUSTOMREQUEST, "POST");
        curl_setopt($url,CURLOPT_RETURNTRANSFER, true);
        curl_setopt($url,CURLOPT_POSTFIELDS, $request_data_json);
        curl_setopt($url,CURLOPT_FOLLOWLOCATION, 1);
        curl_setopt($url, CURLOPT_IPRESOLVE, CURL_IPRESOLVE_V4);
        $result_data = curl_exec($url);
        curl_close($url);

        $response = json_decode($result_data, true);

        return $response;
    }


    private function createPayment(float $totalAmount, string $idToken): object
    {
        $auth = $idToken;
        $requestbody = array(
            'mode' => '0011',
            'amount' => $totalAmount,
            'currency' => 'BDT',
            'intent' => 'sale',
            'payerReference' => '01XXXXXXXXX',
            'merchantInvoiceNumber' => rand(),
            'callbackURL' => $this->callbackURL
        );

        $url = curl_init("$this->base_url/checkout/create");
        $requestbodyJson = json_encode($requestbody);

        $header = array(
            'Content-Type: application/json',
            'Authorization: ' . $auth,
            "X-APP-Key: $this->app_key"
        );


        curl_setopt($url, CURLOPT_HTTPHEADER, $header);
        curl_setopt($url, CURLOPT_CUSTOMREQUEST, "POST");
        curl_setopt($url, CURLOPT_RETURNTRANSFER, true);
        // curl_setopt($url, CURLOPT_SSL_VERIFYPEER, false);
        curl_setopt($url, CURLOPT_POSTFIELDS, $requestbodyJson);
        curl_setopt($url, CURLOPT_FOLLOWLOCATION, 1);
        curl_setopt($url, CURLOPT_IPRESOLVE, CURL_IPRESOLVE_V4);
        $resultdata = curl_exec($url);
        curl_close($url);

        $obj = json_decode($resultdata);

        return $obj;
    }


    public function callback(Request $request)
    {
        if(isset($request->paymentID)){
            if($request->status==="success") {
                $executePaymentObjectData = $this->excecutePayment($request->paymentID);
                if(isset($executePaymentObjectData->statusCode) && in_array($executePaymentObjectData->statusCode, $this->errorCodes)) {
                    $statusCode = $executePaymentObjectData->statusCode;
                    $statusMessage = $executePaymentObjectData->statusMessage;
                    session()->flash('message',"$statusCode | $statusMessage ");
                    
                    return redirect(route("payment.pay.page",'bkash'), 307);
                }

                $this->dataManageAfterSuccessful($executePaymentObjectData->paymentID, $executePaymentObjectData->trxID);

                return redirect(route('payment.success'));
            }
        }

        session()->flash('message','Something Wrong !!!. Payment failed. Please try again later');

        return redirect(route("payment.pay.page",'bkash'), 307);

    }


    private function excecutePayment($paymentID): object
    {
        $auth = json_decode(Session::get('id_token'));

        $post_token = array(
            'paymentID' => $paymentID
        );

        $url = curl_init("$this->base_url/checkout/execute");
        $posttoken = json_encode($post_token);

        $header = array(
            'Content-Type:application/json',
            'Authorization:' . $auth,
            "X-APP-Key: $this->app_key"
        );

        curl_setopt($url, CURLOPT_HTTPHEADER, $header);
        curl_setopt($url, CURLOPT_CUSTOMREQUEST, "POST");
        curl_setopt($url, CURLOPT_RETURNTRANSFER, true);
        curl_setopt($url, CURLOPT_POSTFIELDS, $posttoken);
        curl_setopt($url, CURLOPT_FOLLOWLOCATION, 1);
        curl_setopt($url, CURLOPT_IPRESOLVE, CURL_IPRESOLVE_V4);
        $resultdata = curl_exec($url);

        curl_close($url);

        $obj = json_decode($resultdata);

        return $obj;
    }

    private function dataManageAfterSuccessful($bkashPaymentID, $trxID): void
    {
        // your database related operation
    }

    public function cancel()
    {

    }
}
```
<b>Note : </b> Please look the `afterCreatePayment()` method. You can change your bussiness logic after payment done. Basically in `$this->dataManageAfterSuccessful()` and redirection which is your choice.


### 6. PaymentService class
Create a PaymentService class and then follow the code given below - 

```php

namespace App\Services;

use App\Payment\BkashPayment;
use App\Payment\StripePayment;

class PaymentService
{
    public function initialize($payment_type)
    {
        switch ($payment_type) {
            case 'bkash':
                return new BkashPayment();
            case 'stripe':
                return new StripePayment();
            default:
                break;
        }
    }
}
```

### 7. PaymentController class
create a controller class and follow the code given below -

```php
namespace App\Http\Controllers;

use App\Services\PaymentService;
use Illuminate\Http\Request;
use Illuminate\Support\Facades\Session;

class PaymentController extends Controller
{
    public function checkout(Request $request) 
    {
        return view('payment.checkout');
    }


    public function paymentProcees(Request $request)
    {
        /*
        |--------------------------------------------------------------------------
        | Check your all request validation, filter or apply other condition what you need
        |--------------------------------------------------------------------------
        */
        return redirect(route("payment.pay.page",$request->payment_type), 307);
    }

    public function paymentPayPage($paymentMethod, Request $request)
    {
        // if(gettype($request->requestData) === 'string') {
        //     //during bkash, when it redirects back the bkash page after getting any error. Because this time request was empty
        //     $requestData = $request->requestData;
        //     $request = json_decode($request->requestData);
        // } else {
        //     $requestData = json_encode($request->all());
        // }

        $requestData = json_encode($request->all());
        $totalAmount = $request->price;
        switch ($paymentMethod) {
            case 'bkash':
                $paymentMethodName = "bKash";
                return view('payment.payment_page.bkash',compact('paymentMethodName','requestData','totalAmount'));
            case 'stripe':
                $paymentMethodName = "Stripe";
                return view('payment.payment_page.stripe',compact('paymentMethodName','requestData','totalAmount'));
            default:
                break;
        }
    }


    public function paymentPayConfirm($paymentMethod, Request $request, PaymentService $paymentService) 
    {
        $requestData = json_decode(str_replace('&quot;', '"', $request->requestData));
        if($paymentMethod == 'bkash' || $paymentMethod == 'stripe') {

            $payment = $paymentService->initialize($paymentMethod);
            return $payment->pay($requestData, $request->all());
        }
    }

    public function paymentPayCancel($paymentMethod, PaymentService $paymentService)
    {
        $payment = $paymentService->initialize($paymentMethod);
        return $payment->cancel();
    }

    /*
    |-----------
    |bkash
    |-----------
    */

    public function bkashCallback(PaymentService $paymentService, Request $request)
    {
        $payment = $paymentService->initialize('bkash');
        return $payment->callback($request);
    }

    public function paymentSuccess(Request $request)
    {
        return view('payment.payment_success');
    }

}
```

### 7. blade file

This is one of my checkout page. 

<img src="https://snipboard.io/isvNc0.jpg">


This is my bkash page. 

<img src="https://snipboard.io/h8IqWf.jpg">

Code. This is completely your choice -

```php
@extends('payment.master')
@section('payment')

<div class="row">
    <div class="col-12">
        <h1 class="page-title h2 text-center uppercase mt-1 mb-5">{{ $paymentMethodName }}
            <small>
                ({{ number_format((float)$totalAmount, 2, '.', '') }})
            </small>
        </h1>
    </div>
</div>


@if (session()->has('message'))
    <div class="d-flex justify-content-center">
        <div class="alert alert-danger alert-dismissible fade show" role="alert">
            <strong>{{ session('message')}}!</strong>
            <button type="button" class="btn-close" data-bs-dismiss="alert" aria-label="Close"></button>
        </div>
    </div>
@endif


<div class="row">
    <div class="col-md-3"></div>
    <div class="col-md-6">
        <div class="card">
            <div class="card-body">
                <div class="container-fluid" id="errorMessage"></div>


                <div class="mt-4 d-grid gap-2 mx-auto">
                    <img src="{{ asset('images/payment_logo/bkash.png') }}" height="300px" width="100%">
                </div>

                <form action="{{route('payment.pay.confirm','bkash')}}" method="post">
                    @csrf
                    <input type="hidden" name="requestData" value="{{ $requestData }}">
                    <input type="hidden" name="totalAmount" value="{{ $totalAmount }}">

                    <div class="mt-4 d-grid gap-2 mx-auto">
                        <button type="submit" id="payNowBtn" class="btn btn-outline-success">
                            Pay Now
                            <small>
                                {{ number_format((float)$totalAmount, 2, '.', '') }}
                            </small>
                        </button>
                    </div>
                    <div class="mt-3 d-grid gap-2 mx-auto">
                        <button type="button" id="payCancelBtn" class="btn btn-outline-danger">Cancel</button>
                    </div>
                </form>
            </div>
        </div>
    </div>
</div>
@endsection

```



## References 
- [Bkash Sandbox API Validation](https://www.youtube.com/watch?v=BbuwRxipIY4)
- [Tokenized Developer Docs](https://developer.bka.sh/docs/tokenized-checkout-overview)
