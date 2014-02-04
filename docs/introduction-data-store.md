---
layout: default
title: Introduction
---

Data stores defines an api for persisting uploaded photo details

All data stores implements the interface `DataStoreInterface`

```php
interface DataStoreInterface
{
    public function getConnection();
    public function addPhoto(array $values);
    public function getPhoto($photoId);
    public function getPhotos(array $photoIds);
    public function deletePhoto($photoId);
}
```

All data stores uses a consistent way for setup

```php
new SampleDataStore($connection, array $options);
```

- `$connection`: connection parameters
- `$options`: configuration options
        - `'photo_table'`: set the photo table name

