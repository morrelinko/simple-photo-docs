---
layout: docs
title: File Path Source
---

Photo source uploads from file path.

```php
<?php
use SimplePhoto\Source\FilePathSource;

$simplePhoto->upload(new FilePathSource('/path/to/file.png'));
```

`SimplePhoto` class provides an upload alias for this source

```php
<?php
$simplePhoto->uploadFromFilePath('/path/to/file.png');
```

Use whichever method suits you.