PostcodesIo Laravel Package
============================

[![Build Status](https://travis-ci.org/adityamenon/postcodes-io.svg)](https://travis-ci.org/adityamenon/postcodes-io)

A laravel package for querying the [postcodes.io](http://postcodes.io) web service.

Most of the Guzzle layer code was taken from @BoxUk's [Symfony bundle](https://github.com/BoxUk/postcodes-io-bundle), many props!

[License](LICENSE)

Installation
------------

Installation is handled via [Composer](http://getcomposer.org).

1. Run the following command:
    ```bash
    $ composer require adityamenon/postcodes-io ~1.0
    ```
    This should add the following to your project's `composer.json` file:

    ```js
    "require": {
        "adityamenon/postcodes-io": "~1.0"
    }
    ```
2. Add the Service Provider to your `app/config/app.php` file:

    ```php
    'providers' => array('Adityamenon\PostcodesIo\PostcodesIoServiceProvider')
    ```

3. Add the Facade in the same file:

    ```php
    'aliases' => array('PostcodesIo' => 'Adityamenon\PostcodesIo\Facade')
    ```

Usage
-----

Use the `PostcodesIo` facade with any of the methods below to get data from the service. For example: `PostcodesIo::lookup('CF10 1DD')`.

Methods
-------

lookup()
--------
[API documentation](http://postcodes.io/docs#Postcode-Lookup)

Lookup data about a particular postcode.

__Parameters:__
* `postcode` _(Required)_: The postcode.

__Example:__
```php
$response = $client->lookup(array('postcode' => 'CF10 1DD'));
```


bulkLookup()
--------
[API documentation](http://postcodes.io/docs#Bulk-Postcode-Lookup)

Lookup data about a set of postcodes.

__Parameters:__
* `postcodes` _(Required)_: An array of postcodes (max 100).

__Example:__
```php
$response = $client->bulkLookup(array('postcodes' => array('CF10 1DD', 'W1B 4BD'));
```


reverseGeocode()
--------
[API documentation](http://postcodes.io/docs#Geocode-Postcode)

Get data for postcodes nearest a given latitude/longitude coordinate.

__Parameters:__
* `latitude` _(Required)_: The latitude.
* `longitude` _(Required)_: The longitude.
* `limit` _(Optional)_: The maximum number of postcodes to return (default 10, max 100).
* `radius` _(Optional)_: The radius in metres in which to find postcodes (default 100, max 1000).

__Example:__
```php
$response = $client->reverseGeocode(array('latitude' => 51.481667, 'longitude' => -3.182155);
```


bulkReverseGeocode()
--------
[API documentation](http://postcodes.io/docs#Geocode-Postcode)

Bulk translation of latitude/longitude coordinates into postcode data.

__Parameters:__
* `geolocations` _(Required)_: The geolocations to look up (maximum 100).  This parameter should be an array, each element with the following keys:

    * `latitude` _(Required)_: The latitude.
    * `longitude` _(Required)_: The longitude.
    * `limit` _(Optional)_: The maximum number of postcodes to return (default 10, max 100).
    * `radius` _(Optional)_: The radius in metres in which to find postcodes (default 100, max 1000).

__Example:__
```php
$response = $client->bulkReverseGeocode(
    array(
        'geolocations' => array(
            array('latitude' => 51.481667, 'longitude' => -3.182155),
            array('latitude' => 51.88328, 'longitude' => -3.43684, 'limit' => 5, 'radius' => 500)
        )
    )
);
```


matching()
--------
[API documentation](http://postcodes.io/docs#Postcode-Query)

Find postcodes matching a given query.

__Parameters:__
* `query` _(Optional)_: The postcode query, e.g. 'CF10'.
* `limit` _(Optional)_: The maximum number of postcodes to return (default 10, max 100).

__Example:__
```php
$response = $client->matching(array('query' => 'CF10', 'limit' => 20);
```


validate()
--------
[API documentation](http://postcodes.io/docs#Postcode-Validation)

Validate a postcode.

__Parameters:__
* `postcode` _(Required)_: The postcode to validate.

__Example:__
```php
$response = $client->validate(array('postcode' => 'CF10 1DD');
```


autocomplete()
--------
[API documentation](http://postcodes.io/docs#Postcode-Autocomplete)

Get a list of postcodes to autocomplete a partial postcode.

__Parameters:__
* `postcode` _(Required)_: The postcode to autocomplete.
* `limit` _(Optional)_: The maximum number of postcodes to return (default 10, max 100).

__Example:__
```php
$response = $client->autocomplete(array('postcode' => 'CF10', 'limit' => 20);
```


random()
--------
[API documentation](http://postcodes.io/docs#Random-Postcode)

Get data for a random postcode.

__Parameters:__
None.

__Example:__
```php
$response = $client->random();
```


outwardCodeLookup()
--------
[API documentation](http://postcodes.io/docs#Show-Outcode)

Get data for the specified "outward code" (first half of postcode).

__Parameters:__
* `outcode` _(Required)_: The outward code (first half of postcode) to get location data for.

__Example:__
```php
$response = $client->outwardCodeLookup(array('outcode' => 'CF10');
```
