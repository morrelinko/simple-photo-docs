---
layout: default
title: Url Source
---

Implementation of photo source allowing uploads from web urls

```php
use SimplePhoto\Source\UrlSource;

$simplePhoto->upload(new UrlSource('http://example.com/path/to/image.png'), []);
```
