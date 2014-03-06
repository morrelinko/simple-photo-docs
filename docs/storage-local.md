---
layout: docs
title: Local Storage
---

Save photos to the local file system.

#### Creating local storage

```php
<?php
use SimplePhoto\Storage\LocalStorage;

$localStorage = new LocalStorage(array $options);

```

- `'root'`: Your application public path. Example /var/www/public_html. (required)
- `'path'`: Directory where photo will be saved. This is relative to your 'root' option. (required)


Example:

```php
<?php
use SimplePhoto\Storage\LocalStorage;
use SimplePhoto\StorageManager;
use SimplePhoto\SimplePhoto;

$localStorage = new LocalStorage([
    'root' => '/www/public_html/',
    'path' => 'files/photos'
]);

$storageManager = new StorageManager();
$storageManager->add('my_local_storage', $localStorage);

$simplePhoto = new SimplePhoto($storageManager, $dataStore);
```
