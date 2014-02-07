---
layout: default
title: Installation
---

### Requirements

* PHP 5.3+

This library can be installed through [Composer](http://getcomposer.org)  [Recommended]

{% highlight json %}
{
    "require": {
        "morrelinko/simple-photo": "2.1.0"
    }
}
{% endhighlight %}

Or manually by loading the *autoloader* that came with simple-photo

{% highlight php %}
require_once '/path/to/simple-photo/autoload.php';
{% endhighlight %}

Note: This library depends on the [Imagine](https://packagist.org/packages/imagine/imagine)
library for image transformation

### Setup

```php
use SimplePhoto\Store\DataStore;
use SimplePhoto\Storage\LocalStorage;
use SimplePhoto\SimplePhoto;
use SimplePhoto\StorageManager;

// Setup data store (photo details will be saved here)
$dataStore = new SqliteDataStore(['database' => 'path/to/sample_app.db']);

// Setup storage (photo files will be saved here)
$localStorage = new LocalStorage('/path/to/project/root', 'files/user/pic');

// Setup storage
$storageManager = new StorageManager();

// Add one or more storage
$storageManager->add('local_user_pic', $localStorage);

//
$simplePhoto = new SimplePhoto($storageManager, $dataStore);

```