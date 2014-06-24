# A PHP MongoDB query builder library

## Install via Packagist and Composer

Add the following into your composer.json file:

```javascript
{
	"require": {
		"jumplead/mongoqb": "*"
	}
}
```

Then run

```bash
composer install
```

## Install via Git

```bash
git clone git://git@github.com:jumplead/MongoQB
```

## Download a zip/tarball

Download the latest version:

* [zip](https://github.com/jumplead/MongoQB/archive/master.zip)
* [tar](https://github.com/jumplead/MongoQB/archive/master.tar.gz)

(Note the zip/tarball won't include any unit tests or composer files)

## Unit tests

Master branch [![Build Status](https://travis-ci.org/Jumplead/MongoQB.svg)

The library currently has 100% unit test coverage. To run the unit test suite make sure you have MongoDB installed locally and running with no authentication and on the default port - 27017.

Then run:

```bash
composer update --dev
cd vendor/jumplead/mongoqb
phpunit -c tests/phpunit.xml
```

## Example usage

### Connect to the database

```php
$qb = \MongoQB\Builder(array(
	'dsn'	=>	'mongodb://user:pass@localhost:27017/databaseName'
);
```

### Insert a document

```php
$qb->insert('collectionName', [
	'name'	=>	'Alex',
	'age'	=>	22,
	'likes'	=>	['whisky', 'gin']
]);
```

### Update a single document

```php
$qb
	->where(['name' => 'Alex'])
	->set([
		'country' => 'UK',
		'job' => 'Developer'
	])
	->push('likes', ['PHP', 'coffee'])
	->update('collectionName');
```

### Delete a single document

```php
$qb
	->where(['name' => 'Alex'])
	->delete('collectionName');
```

### Search for matching documents

```php
$results = $qb
	->whereGt('age', 21)
	->whereIn('likes', ['whisky'])
	->where('country', 'UK')
	->get('collectionName');
```

If you find any bugs please file a report in the [Issue tracker](https://github.com/jumplead/MongoQB/issues)
