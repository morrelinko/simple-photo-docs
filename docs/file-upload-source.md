---
layout: default
title: File Upload Source
---

Implementation of photo source allowing uploads from PHP File Uploads

```php
use SimplePhoto\Source\PhpFileUploadSource;

$simplePhoto->upload($_FILES['image'], new PhpFileUploadSource(), []);
```

An alias in already exists for this in the SimplePhoto class

```php
use SimplePhoto\SimplePhoto;

$simplePhoto->uploadFromPhpFileUpload($_FILES['image'], []);
```

Use whichever method suits you.
