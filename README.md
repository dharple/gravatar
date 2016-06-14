# Gravatar

[![Latest Version](https://img.shields.io/github/release/gravatarphp/gravatar.svg?style=flat-square)](https://github.com/gravatarphp/gravatar/releases)
[![Software License](https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square)](LICENSE)
[![Build Status](https://img.shields.io/travis/gravatarphp/gravatar.svg?style=flat-square)](https://travis-ci.org/gravatarphp/gravatar)
[![Code Coverage](https://img.shields.io/scrutinizer/coverage/g/gravatarphp/gravatar.svg?style=flat-square)](https://scrutinizer-ci.com/g/gravatarphp/gravatar)
[![Quality Score](https://img.shields.io/scrutinizer/g/gravatarphp/gravatar.svg?style=flat-square)](https://scrutinizer-ci.com/g/gravatarphp/gravatar)
[![Total Downloads](https://img.shields.io/packagist/dt/gravatarphp/gravatar.svg?style=flat-square)](https://packagist.org/packages/gravatarphp/gravatar)

**Gravatar URL builder which is most commonly called as a Gravatar library.**


## Install

Via Composer

``` bash
$ composer require gravatarphp/gravatar
```


## Usage

Create a `UrlBuilder` instance and use it for creating URLs.

``` php
use Gravatar\UrlBuilder;

// Defaults: no default parameter, use HTTPS
$urlBuilder = new UrlBuilder([], true);

// Returns https://secure.gravatar.com/avatar/EMAIL_HASH
$urlBuilder->avatar('user@domain.com');

// Returns https://secure.gravatar.com/EMAIL_HASH
$urlBuilder->profile('user@domain.com');

// Returns https://secure.gravatar.com/EMAIL_HASH.vcf
$urlBuilder->vcard('user@domain.com');

// Returns https://secure.gravatar.com/EMAIL_HASH.qr
$urlBuilder->qrCode('user@domain.com');
```


Or use the static version.

``` php
use Gravatar\StaticUrlBuilder as Gravatar;

// Optional
Gravatar::configure([], true);

// Returns https://secure.gravatar.com/avatar/EMAIL_HASH
Gravatar::avatar('user@domain.com');

// Returns https://secure.gravatar.com/EMAIL_HASH
Gravatar::profile('user@domain.com');

// Returns https://secure.gravatar.com/EMAIL_HASH.vcf
Gravatar::vcard('user@domain.com');

// Returns https://secure.gravatar.com/EMAIL_HASH.qr
Gravatar::qrCode('user@domain.com');
```


You can also use the `SingleUrlBuilder` which accepts an email in its constructor.

``` php
use Gravatar\SingleUrlBuilder;

// Email
// No default parameters (optional)
// Use HTTPS (optional)
$urlBuilder = new SingleUrlBuilder('user@domain.com', [], true);

// Returns https://secure.gravatar.com/avatar/EMAIL_HASH
$urlBuilder->avatar();

// Returns https://secure.gravatar.com/EMAIL_HASH
$urlBuilder->profile();

// Returns https://secure.gravatar.com/EMAIL_HASH.vcf
$urlBuilder->vcard();

// Returns https://secure.gravatar.com/EMAIL_HASH.qr
$urlBuilder->qrCode();
```


In all three URL Bulders you can override the globally used protocol (HTTP, HTTPS) by setting the last parameter to
true/false.

``` php
use Gravatar\UrlBuilder;

$urlBuilder = new UrlBuilder();

// Returns http://www.gravatar.com/avatar/EMAIL_HASH
$urlBuilder->avatar('user@domain.com', [], false);

// Returns http://www.gravatar.com/EMAIL_HASH
$urlBuilder->profile('user@domain.com', false);

// Returns http://www.gravatar.com/EMAIL_HASH.vcf
$urlBuilder->vcard('user@domain.com', false);

// Returns http://www.gravatar.com/EMAIL_HASH.qr
$urlBuilder->qrCode('user@domain.com', false);
```


Last, but not least, you can pass default parameters to the builders...

``` php
use Gravatar\UrlBuilder;
use Gravatar\StaticUrlBuilder as Gravatar;
use Gravatar\SingleUrlBuilder;

$urlBuilder = new UrlBuilder([
    'size' => 500,
]);

$urlBuilder = new SingleUrlBuilder(
    'user@domain.com',
    [
        'size' => 500,
    ]
);

Gravatar::configure([
    'size' => 500,
]);
```


...and use them to generate avatar URLs.

``` php
// Returns https://secure.gravatar.com/avatar/EMAIL_HASH?size=500&r=g
$urlBuilder->avatar('user@domain.com', ['r' => 'g']);
```


**Note:** Parameters are not sanitized or validated in anyway. For valid parameters check the [Gravatar documentation](http://gravatar.com/site/implement/).


**Note:** Profile, vCard and QR Code requests will only work with the primary email address. This is a limitation of Gravatar. However the builder won't complain, since it doesn't know if it is your primary address or not. For more tips and details check the [Gravatar documentation](http://gravatar.com/site/implement/).


## Testing

``` bash
$ composer test
```


## Credits

- [Márk Sági-Kazár](https://github.com/sagikazarmark)
- [All Contributors](https://github.com/gravatarphp/gravatar/contributors)


## License

The MIT License (MIT). Please see [License File](LICENSE) for more information.
