---
layout: docs
title: Sqlite Data Store
---

```php
<?php
use SimplePhoto\DataStore\SqliteDataStore;

$dataStore = new SqliteDataStore(array(
    'database' => 'sample_app.db'
));

```

Or by passing an instance of a PDO connection

```php
<?php
use SimplePhoto\DataStore\SqliteDataStore;

$pdo = new \PDO('sqlite:' . $path);
$dataStore = new SqliteDataStore($pdo);
```
