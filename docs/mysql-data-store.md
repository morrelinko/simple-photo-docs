---
layout: default
title: Mysql Data Store
---

```php
use SimplePhoto\DataStore\MysqlDataStore;

$dataStore = new MysqlDataStore([
    'host' => '127.0.0.1',
    'database' => 'sample_app',
    'username' => 'johndoe',
    'password' => 'pa$$word'
]);

```

Or by passing an instance of a PDO connection

```php
use SimplePhoto\DataStore\MysqlDataStore;

$pdo = new \PDO(
    'mysql:host=127.0.0.1;dbname=sample_app',
    'johndoe',
    'pa$$word'
);

$dataStore = new MysqlDataStore($pdo);
```
