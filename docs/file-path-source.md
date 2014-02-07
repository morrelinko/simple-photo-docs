---
layout: default
title: File Path Source
---

Implementation of photo source allowing uploads from file paths

```php
use SimplePhoto\Source\FilePathSource;

$simplePhoto->upload('/path/to/file.png', new FilePathSource(), []);
```

An alias in already exists for this in the SimplePhoto class

```php
$simplePhoto->uploadFromFilePath('/path/to/file.png', []);
```

Use whichever method suits you.