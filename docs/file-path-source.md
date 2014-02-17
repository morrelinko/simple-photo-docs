---
layout: default
title: File Path Source
---

Implementation of photo source allowing uploads from file paths

```php
use SimplePhoto\Source\FilePathSource;

$simplePhoto->upload(new FilePathSource('/path/to/file.png'), []);
```

`SimplePhoto` class provides an upload alias for this source

```php
$simplePhoto->uploadFromFilePath('/path/to/file.png', []);
```

Use whichever method suits you.