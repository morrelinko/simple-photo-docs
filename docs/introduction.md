---
layout: default
title: Introduction
---

Simple Photo - Photo management made easy

### Goals

- Reduced boiler plate
- Different Input Sources
- Different Storage Locations
- Quickly transform photo
- Display Fallback Images if for invalid images

[Under Construction]

#### Different Input Sources

No need for converting from one file source to another before uploading,

Different implementations for those sources are available (implementing yours is breeze)

```php
$simplePhoto->uploadFromFilePath('/path/to/image.png');
$simplePhoto->uploadFromPhpFileUpload($_FILES['image']);
$simplePhoto->uploadFrom($source, PhotoSourceInterface $source, array $options);
```

#### Different Storage Locations

```php
$storageManager->add('user_profile_photos', $yourStorageForUserProfilePhotos);
$storageManager->add('forum_attachment_photos', $yourStorageForAttachedForumPhotos);
```

#### Quickly Transform photo

```html+php
<img src="<?php echo $simplePhoto->get(1, ['transform' => ['size' => [200, 200]]])->url(); ?>" />
```

#### Fallback Photo

```php
$storageManager->setFallback($yourStorageForStoringFallbackPhoto);

// Example: Get user
$simplePhoto->get(1, ['fallback' => 'user_default.png']);

// Example: Get User Cover Photo
$simplePhoto->get(2, ['fallback' => 'user_cover_default.png']);
```

