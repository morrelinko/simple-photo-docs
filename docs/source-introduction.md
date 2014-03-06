---
layout: docs
title: Introduction
---

Upload Sources implements a `PhotoSourceInterface`

```php
<?php
interface PhotoSourceInterface
{
    public function process($photoData);
    public function getName();
    public function getFile();
    public function getMime();
    public function isValid();
}
```

Currently supported photo sources

* [FilePathSource](/docs/source-file-path)
* [PhpFileUploadSource](/docs/source-file-upload)
* [UrlSource](/docs/source-url)

