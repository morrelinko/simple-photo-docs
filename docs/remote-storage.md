---
layout: default
title: Remote Storage
---

This allows for saving photos in a different domain.

#### Adding Remote host storage: Syntax

```php

use SimplePhoto\Storage\LocalStorage;

$localStorage = new LocalStorage($photoPath, $host, array $options);

```

- `$photoPath`: Directory where photo will be saved on the domain.
- `$host`: Your FTP Host name (The Remote Host storage uses ftp protocol internally)
- `$options`: Available Options
    - `'root'`: Ftp Root path eg '/'
    - `'url'`: The domain name eg 'http://static.img-ex.com
    - `'username'`: Ftp username (Optional, Defaults to anonymous if not specified)
    - `'password'`: Ftp password (Optional, defaults to '' if not specified)
    - `'port'`: Ftp Port (defaults to 21 if not specified)

Example:

```php

use SimplePhoto\Storage\RemoteHostStorage;
use SimplePhoto\StorageManager;
use SimplePhoto\SimplePhoto;

$remoteHostStorage = new RemoteHostStorage('/files/photos/', '127.0.0.1', [
    'root' => '/',
    'url' => 'http://static.img-ex.com',
    'username' => 'joeftpd',
    'password' => 'pa$$word',
    'port' => 21
]);

$storageManager = new StorageManager();
$storageManager->add('img_static_storage', $remoteHostStorage);

$simplePhoto = new SimplePhoto($storageManager, $dataStore);
```
