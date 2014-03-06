---
layout: docs
title: Installation
---

### Requirements

* PHP 5.3+
* GD Library

This library can be installed through [Composer](http://getcomposer.org)  [Recommended]

```json
{
    "require": {
        "morrelinko/simple-photo": "0.4.*"
    }
}
```

Or manually by loading the *autoloader* that comes with simple photo library

```php
<?php
require_once '/path/to/simple-photo/autoload.php';
```

Manual Installation Note: This library depends on the [Imagine](https://packagist.org/packages/imagine/imagine)
library for image transformation

### Setup

```php
<?php
use SimplePhoto\Store\DataStore;
use SimplePhoto\Storage\LocalStorage;
use SimplePhoto\SimplePhoto;
use SimplePhoto\StorageManager;

// Setup data store
$dataStore = new SqliteDataStore(['database' => 'path/to/sample_app.db']);

// Setup storage
$localStorage = new LocalStorage([
    'root' => '/path/to/public_html',
    'path' => 'files/user/pic'
]);

// Setup storage
$storageManager = new StorageManager();

// Add one or more storage
$storageManager->add('local', $localStorage);

$simplePhoto = new SimplePhoto($storageManager, $dataStore);
```