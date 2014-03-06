---
layout: docs
title: Introduction
---

Simple Photo - Photo management made easy

### Goals

- Reduce boiler plate codes and complexities when working with photos in your application.
- Play nicely with other packages/frameworks.
- Support uploading photos from different sources.
- Support saving photos to different storage locations.
- Make it easy to transform photos before upload and/or on-the-fly when retrieving.
- Support using a fallback/default photo.
- Support getting details about a photo.

#### Different Input Sources

```php
<?php
$simplePhoto->upload(new UrlSource('http://example.com/path/to/image.png'));
$simplePhoto->upload(new PhpFileUploadSource($_FILES['image']));
$simplePhoto->upload(new FilePathSource('/path/to/photo.png'));
```

#### Different Storage Locations

```php
<?php
$localUserPhotos = new LocalStorage(...);
$localForumPhotos = new LocalStorage(...);

$storageManager->add('user_photos', $localUserPhotos);
$storageManager->add('forum_photos', $localForumPhotos);
```

#### Transform photo
```html+php
<?php
// On Upload
$simplePhoto->upload(new PhpFileUploadSource($_FILES['image']), [
    'transform' => [
        'size' => [200, 200]
    ]
]);
?>

<!-- Instantly on the fly transformation -->
<img src="<?php echo $simplePhoto->get($id, ['transform' => ['size' => [200, 200]]])->url(); ?>" />
```

#### Fallback Photo

```php
<?php
$fallbackStorage = new LocalStorage();
$storageManager->setFallback($fallbackStorage);

// Example: Get user
$simplePhoto->get(1, ['fallback' => 'user_default.png']);

// Example: Get User Cover Photo
$simplePhoto->get(2, ['fallback' => 'user_cover_default.png']);
```

