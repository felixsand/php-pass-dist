# PhPsst

A PHP library for distributing (one time) passwords/secrets in a more secure way

## Installation
Add the package as a requirement to your `composer.json`:
```bash
$ composer require felixsand/PhPsst
```

## Usage
```php
<?php
use PhPsst\PhPsst;
use PhPsst\Storage\FileStorage;

$phPsst = new PhPsst(new FileStorage('data/passwords', 10));
$secret = $phPsst->store('my secret password');
echo "The passwords ID and encryption key: {$secret}\n";
echo "The password: {$phPsst->retrieve($secret)}\n";
```

## Storage Classes
### FileStorage
The most basic of the storage classes is the FileStorage. It's also (generally) the most insecure and if you store a lot
of passwords there's a performance issue due to the garbage collector being very crude. It is however the easiest way
to try out the library and useful during development.

### RedisStorage
The recommended production storage class is the RedisStorage. It has great performance even during heavy use and
since it removes the passwords with expired TTL automatically, it's more secure than the other options.
It's important to note that if you're not reviewing the Redis configuration, it might purge entries even before the
item's TTL has expired (if it's memory limit is reached) and the items will only live for as long as the server is
running. This might be desired properties in certain cases, but you need to be aware of it when setting up the solution.

## Requirements
- PHP 5.6 or above.
- Redis

## Author
Felix Sandström <http://github.com/felixsand>

## License
Licensed under the MIT License - see the `LICENSE` file for details.
