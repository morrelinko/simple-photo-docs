---
layout: docs
title: Remote Storage
---

Save photos to a remote host.


#### Creating remote storage

```php
<?php
use SimplePhoto\Storage\RemoteHostStorage;

$remoteStorage = new RemoteHostStorage(array $options);

```

- `$options`: Available Options
    - `'host'`: Your FTP Host name (The Remote Host storage uses ftp protocol internally) (required)
    - `'root'`: Ftp Root path eg '/'
    - `'path'`: Directory where photo will be saved on the domain. (required)
    - `'url'`: The domain name eg 'http://static.img-ex.com (required)
    - `'username'`: Ftp username (Optional, Defaults to anonymous if not specified)
    - `'password'`: Ftp password (Optional, defaults to '' if not specified)
    - `'port'`: Ftp Port (defaults to 21 if not specified)

Example:

```php
<?php
use SimplePhoto\Storage\RemoteHostStorage;
use SimplePhoto\StorageManager;
use SimplePhoto\SimplePhoto;

$remoteHostStorage = new RemoteHostStorage(, [
    'host' => '127.0.0.1',
    'root' => '/',
    'path' => '/files/photos/',
    'url' => 'http://static.img-ex.com',
    'username' => 'joeftpd',
    'password' => 'pa$$word',
    'port' => 21
]);

$storageManager = new StorageManager();
$storageManager->add('img_static_storage', $remoteHostStorage);

$simplePhoto = new SimplePhoto($storageManager, $dataStore);
```
