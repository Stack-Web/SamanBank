# SamanBank
[![Software License](https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square)](LICENSE.md)

Saman bank payment package

### Install

Install latest version using [composer](https://getcomposer.org/).

``` bash
$ composer require sadegh-pm/saman_bank
```
### Usage
Request payment:
```php
<?php
use SadeghPM\SamanBank\Saman;
use SadeghPM\SamanBank\SamanStorageAdapterInterface;
//seller ID
$merchantId = 'xxxxxxxx';
//database storage adapter that implements SamanStorageAdapterInterface
$myStorageAdapter = new myImplimentedStorageAdapter();
$payment = new Saman($myStorageAdapter,$merchantId);

$amountInRial = 10000;
//return customer after payment
$callbackUrl = 'http://mysite.ir/callback';
//request payment and redirect user to saman payment page
echo $payment->payRequest($amountInRial,$callbackUrl)->getRedirectScript();
```

Response verify:
```php
<?php
use SadeghPM\SamanBank\Saman;
use SadeghPM\SamanBank\SamanStorageAdapterInterface;
//seller ID
$merchantId = 'xxxxxxxx';
//database storage adapter that implements SamanStorageAdapterInterface
$myStorageAdapter = new myImplimentedStorageAdapter();
$payment = new Saman($myStorageAdapter,$merchantId);

try{
    $payment->getPayStat($_POST);
    echo 'Thanks...successful payment.';
}catch (\Throwable $throwable){
    echo "error :".$throwable->getMessage();
}
```