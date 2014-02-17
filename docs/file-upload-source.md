---
layout: default
title: File Upload Source
---

Implementation of photo source allowing uploads from PHP File Uploads

```php
use SimplePhoto\Source\PhpFileUploadSource;

$simplePhoto->upload(new PhpFileUploadSource($_FILES['image']), []);
```

SimplePhoto class provides an alias for this source

```php
use SimplePhoto\SimplePhoto;

$simplePhoto->uploadFromPhpFileUpload($_FILES['image'], []);
```

Use whichever method suits you.
