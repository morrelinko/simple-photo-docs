---
layout: docs
title: File Upload Source
---

Photo source uploads from php file uploads (_FILES)

```php
<?php
use SimplePhoto\Source\PhpFileUploadSource;

$simplePhoto->upload(new PhpFileUploadSource($_FILES['image']));
```

SimplePhoto class provides an alias for this source

```php
<?php
use SimplePhoto\SimplePhoto;

$simplePhoto->uploadFromPhpFileUpload($_FILES['image']);
```

Use whichever method suits you.
