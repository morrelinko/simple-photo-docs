---
layout: default
title: Introduction to Input Sources
---

Input sources are objects implementing a `PhotoSourceInterface`

abstracting uploaded photo sources.

This allows for photo files to be uploaded from different locations.

```php
interface PhotoSourceInterface
{
    public function process($photoData);
    public function getName();
    public function getFile();
}
```

Currently, two photo source implementation exists

* [FilePathSource](/docs/file-path-source/)
* [PhpFileUploadSource](/docs/file-upload-source/)

