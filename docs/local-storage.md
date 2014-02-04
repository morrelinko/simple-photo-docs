---
layout: default
title: Local Storage
---

This allows saving photos in the local file system that your script is running.

#### Adding local storage: Syntax

```php

use SimplePhoto\Storage\LocalStorage;

$localStorage = new LocalStorage($projectRootPath, $photoPath);

```

- `$projectPath`: Your application root path. Basically the directory that contains your public index.php file.
- `$photoPath`: Directory where photo will be saved. This is relative to your


Example:

```php

use SimplePhoto\Storage\LocalStorage;
use SimplePhoto\StorageManager;
use SimplePhoto\SimplePhoto;

$localStorage = new LocalStorage('/www/public_html/', 'files/photos');

$storageManager = new StorageManager();
$storageManager->add('my_local_storage', $localStorage);

$simplePhoto = new SimplePhoto($storageManager, $dataStore);
```
