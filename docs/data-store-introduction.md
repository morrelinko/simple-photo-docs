---
layout: docs
title: Introduction
---

Data stores defines an api for persisting uploaded photo details

All data stores implements the interface `DataStoreInterface`

```php
<?php
interface DataStoreInterface
{
    public function getConnection();
    public function addPhoto(array $values);
    public function getPhoto($photoId);
    public function getPhotos(array $photoIds);
    public function deletePhoto($photoId);
}
```

Supported Data Stores

* [SQLite](/docs/data-store-sqlite)
* [MySQL](/docs/data-store-mysql)
