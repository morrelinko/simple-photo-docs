---
layout: docs
title: The Library
---

## Uploading

```php
<?php
$simplePhoto->upload(new PhpFileUploadSource($_FILES['image']));
```

When you upload a photo, you get a unique ID for that photo.

this is the ID you attach to an entity in your application.

For example, 'photo_id' column on users table

```php
<?php
// Example template code
$photoId = $simplePhoto->upload(...);

$db->update($userId, ['photo_id' => $photoId]);
```

#### Setting storage location
The first storage added to the storage manager is used by default.

If you added more than one storage locations to your storage manager,

you can use the `'storage_name'` option to explicitly define the storage location to save the

photo. This value takes the name that was used when adding the storage.

```php
<?php
$storageManager = new StorageManager();
$storageManager->add('other_storage', new RemoteHostStorage(...)):

$simplePhoto->upload(new PhpFileUploadSource($_FILES['image']), [
    'storage_name' => 'other_storage'
]);
```

#### Transforming on upload

You can perform some image transformation during upload using the `'transform'` option

```php
<?php

$simplePhoto->upload(new PhpFileUploadSource($_FILES['image']), [
    'transform' => [
        'resize' => [150, 150],
        'rotate' => [180]
    ]
]);
```

## Working with Photos

#### Retrieving photo

```php
<?php
$photo = $simplePhoto->get($photoId);
```

The value returned is a `SimplePhoto\PhotoResult` object which can be used to

get various information about a photo

```php
<?php
$photo = $simplePhoto->get($photoId);

echo $photo->id();
echo $photo->url();
echo $photo->path();
echo $photo->originalPath();
echo $photo->createdAt();
echo $photo->updatedAt();
echo $photo->storage();
echo $photo->fileMime();
echo $photo->filePath();
echo $photo->fileSize();
echo $photo->fileExtension();
```

#### Transform photo when retrieving

You can also transform photo when retrieving by passing a `'transform'` option to the section argument

```php
<?php
$photo = $simplePhoto->get($photoId, [
    'transform' => [
        'size' => [300, 200]
    ]
]);
```

An example use case showing how useful this can be..

```php
<img src="<?php echo $simplePhoto->get($photoId, ['transform' => ['size' => ['150', '150']]])->url(); ?>" />
```

Transformation is performed on the fly and photo is cached permanently so subsequent requests won't

perform photo transformation.

## Photo Collection

When you perform a `get($photoId)` simple photo looks up a data store

to retrieve the photo performing a query in the process.

Consider this example:

```php
<?php
foreach ($users as $user) {
    echo 'Photo: ' . $simplePhoto->get($user['photo_id']);
}
```

If the number of users we are looping through = N, This code above will execute N queries

Thankfully, `collection()` in simple photo helps to reduce the no. of queries.

```php
<?php
// $photos = $simplePhoto->collection($ids, array $options);

$photos = $simplePhoto->collection([10, 12, 34, 53, 3, 343, 12003, 436]);
```

The above code will execute one data store lookup and build a collection of photos.

The value returned is a `SimplePhoto\PhotoCollection` object

#### Retrieving photo from photo collection

Photos are accessed in the order which they were added

```php
<?php
$photo = $photos->get(0); // Gets photo with #ID 10
$photo = $photos->get(2); // Gets photo with #ID 34

...
```

## Push

This is a feature in Simple Photo that allows you to push photo result or details about a photo

into an already existing array or array of items.

Consider the following data.

```php
<?php

// Probably gotten from db or api or something
$users = [
    [
        'name' => 'John Doe',
        'photo_id' => 20354634,
    ],
    [
        'name' => 'Alice Bored',
        'photo_id' => 876532324
    ]
];
```

You can add photo elements with ease using the `push()` method

```php
<?php

$users = [...]; // Same data as above code

$simplePhoto->push($users);

// The $users becomes

$users = [
    [
        'name' => 'John Doe',
        'photo_id' => 20354634,
        'photo' => (Object) PhotoResult
    ],
    [
        'name' => 'Alice Bored',
        'photo_id' => 876532324,
        'photo' => (Object) PhotoResult
    ]
];
```

By convention, if no keys are defined, push() method searches for 'photo_id' in each element and uses

that to build the photo result. But if you use a different column name, you can specify this by

passing a second argument to the push() method.

```php
<?php

$users = [
    [
        'name' => 'John Doe',
        'profile_pic' => 20354634
    ],
    [
        'name' => 'Alice Bored',
        'profile_pic' => 876532324
    ]
];

$simplePhoto->push($users, ['profile_pic']);
```

If you have more than one columns to build photos for, you can pass add them to the second argument.

```php
<?php

$users = [
    [
        'name' => 'John Doe',
        'profile_id' => 20354634,
        'cover_photo_id' => 4109832789
    ],
    [
        'name' => 'Alice Bored',
        'profile_id' => 876532324,
        'cover_photo_id' => 280986790
    ]
];

$simplePhoto->push($users, ['profile_id', 'cover_photo_id']);
```

Don't want the whole photo object added to the array, Don't worry, `push()` gives you control

over what is added to the array. Pass a callback as a third argument and put your logic there.

```php
<?php

$users = [
    [
        'name' => 'John Doe',
        'profile_id' => 20354634
    ],
    [
        'name' => 'Alice Bored',
        'profile_id' => 876532324
    ]
];

// NOTE: the & (reference) symbol. This is required to that the item in the original photo is updated
$simplePhoto->push($users, ['profile_id'], function(&$item, PhotoResult $photo, $name, $index) {
    $item['profile_pic_url'] = $photo->url();
});

// You get an array like this

$users = [
     [
         'name' => 'John Doe',
         'profile_id' => 20354634,
         'profile_pic_url' => 'http://example.com/files/photo.png'
     ],
     [
         'name' => 'Alice Bored',
         'profile_id' => 876532324,
         'profile_pic_url' => 'http://example.com/files/photo.png'
     ]
 ];
```

For multiple photos fields

```php
<?php
$users = [
    [
        'name' => 'John Doe',
        'profile_id' => 20354634,
        'cover_photo_id' => 98764758697
    ],
    [
        'name' => 'Alice Bored',
        'profile_id' => 876532324,
        'cover_photo_id' => 280986790
    ]
];

$simplePhoto->push(
    $users,
    ['profile_id', 'cover_photo_id'],
    function(&$item, PhotoResult $photo, $name, $index) {
        if ($index == 'profile_id') {
            // Check if `push()` is building photos for 'profile_id' column
            $item['profile_pic_url'] = $photo->url();
        } else if ($index == 'cover_photo_id') {
            // Check if `push()` is building photos for 'cover_photo_id' column
            $item['cover_photo_url'] = $photo->url();
        }
    }
);

// You get this
[
    [
        'name' => 'John Doe',
        'profile_id' => 20354634,
        'cover_photo_id' => 98764758697,
        'profile_pic_url' => 'http://example.com/files/photo.png',
        'cover_photo_url' => 'http://example.com/files/cover.png'
    ],
    [
        'name' => 'Alice Bored',
        'profile_id' => 876532324,
        'cover_photo_id' => 280986790,
        'profile_pic_url' => 'http://example.com/files/photo.png',
        'cover_photo_url' => 'http://example.com/files/cover.png'
    ]
];