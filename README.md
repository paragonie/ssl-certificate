# A class to validate SSL certificates

[![Latest Version on Packagist](https://img.shields.io/packagist/v/spatie/ssl-certificate.svg?style=flat-square)](https://packagist.org/packages/spatie/ssl-certificate)
[![Software License](https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square)](LICENSE.md)
[![Build Status](https://img.shields.io/travis/spatie/ssl-certificate/master.svg?style=flat-square)](https://travis-ci.org/spatie/ssl-certificate)
[![SensioLabsInsight](https://img.shields.io/sensiolabs/i/533fbcef-7363-41af-8d1c-ab53bb6a1d76.svg?style=flat-square)](https://insight.sensiolabs.com/projects/533fbcef-7363-41af-8d1c-ab53bb6a1d76)
[![Quality Score](https://img.shields.io/scrutinizer/g/spatie/ssl-certificate.svg?style=flat-square)](https://scrutinizer-ci.com/g/spatie/ssl-certificate)
[![Total Downloads](https://img.shields.io/packagist/dt/spatie/ssl-certificate.svg?style=flat-square)](https://packagist.org/packages/spatie/ssl-certificate)

The class provided by this package makes it incredibly easy to query the properties on an ssl certificate. Here's an example:

```php
$certificate = SslCertificate::createForHostName('spatie.be');

$certificate->getIssuer(); // returns "Let's Encrypt Authority X3"
$certificate->isValid(); // returns true if the certificate is currently valid
$certificate->getExpirationDate(); // returns an instance of Carbon
$certificate->getExpirationDate()->diffInDays(); // returns an int
```

Spatie is a webdesign agency based in Antwerp, Belgium. You'll find an overview of all our open source projects [on our website](https://spatie.be/opensource).

## Installation

You can install the package via composer:

```bash
composer require spatie/ssl-certificate
```

## Important notice

Currently this package [does not check](https://github.com/spatie/ssl-certificate/blob/master/src/SslCertificate.php#L63-L74) if the certificate is signed by a trusted authority. We'll add this check soon in a next point release.

## Usage

You can create an instance of `Spatie\SslCertificate\SslCertificate` with this named constructor:

```php
$certificate = SslCertificate::createForHostName('spatie.be');
```

If the given `hostName` is invalid `Spatie\SslCertificate\InvalidUrl` will be thrown.

If the given `hostName` is valid but there was a problem downloading the certifcate `Spatie\SllCertificate\CouldNotDownloadCertificate` will be thrown.

### Getting the issuer name

```php
$certificate->getIssuer(); // returns "Let's Encrypt Authority X3"
```

### Getting the domain name

Returns the primary domain name for the certificate

```php
$certificate->getDomain(); // returns "spatie.be"
```

### Getting the additional domain names

A certificate can cover multiple (sub)domains. Here's how to get them.

```php
$certificate->getAdditionalDomains(); // returns ["spatie.be", "www.spatie.be]
```

A domain name return with this method can start with `*` meaning it is valid for all subdomains of that domain.

### Getting the date when the certificate becomes valid

```php
$this->certificate->validFromDate(); // returns an instance of Carbon
```

### Getting the expiration date

```php
$this->certificate->expirationDate(); // returns an instance of Carbon
```

### Determining if the certificate is still valid

Returns true if the current Date and time is between `validFromDate` and `expirationDate`.

```php
$this->certificate->isValid(); // returns a boolean
```

You also use this method to determine if a given domain is covered by the certificate. Of course it'll keep checking if the current Date and time is between `validFromDate` and `expirationDate`.

```php
$this->certificate->isValid('spatie.be'); // returns true;
$this->certificate->isValid('laravel.com'); // returns false;
```

## Changelog

Please see [CHANGELOG](CHANGELOG.md) for more information what has changed recently.

## Testing

``` bash
$ composer test
```

## Contributing

Please see [CONTRIBUTING](CONTRIBUTING.md) for details.

## Security

If you discover any security related issues, please email freek@spatie.be instead of using the issue tracker.

## Credits

- [Freek Van der Herten](https://github.com/freekmurze)
- [All Contributors](../../contributors)

The helper functions and tests were copied from the [Laravel Framework](https://github.com/laravel/framework).

## About Spatie
Spatie is a webdesign agency based in Antwerp, Belgium. You'll find an overview of all our open source projects [on our website](https://spatie.be/opensource).

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.
