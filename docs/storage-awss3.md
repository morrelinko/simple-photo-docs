---
layout: docs
title: AwsS3 Storage
---

Save photos to the aws.

#### Creating the Storage

```php
<?php

use Aws\S3\S3Client;
use SimplePhoto\Storage\AwsS3Storage;

$localStorage = new AwsS3Storage(S3Client $client, array $options);

```

Available `$options`

- `'bucket'`: Bucket name (required)
- `'directory'`: A directory like prefix that is prepended to stored photos. (optional)
- `'acl'`: ACL, Defaults to 'public-read' (optional)


Example:

```php
<?php

use Aws\S3\S3Client;
use SimplePhoto\Storage\AwsS3Storage;
use SimplePhoto\StorageManager;
use SimplePhoto\SimplePhoto;

$client = S3Client::factory(array(
    'key' => 'Your_Key',
    'secret' => 'Your_Secret',
));

$awsS3Storage = new AwsS3Storage($client, [
    'bucket' => 'bucket-name',
    'directory' => 'optional-file-prefix'
]);

$storageManager = new StorageManager();
$storageManager->add('aws_storage', $awsS3Storage);

$simplePhoto = new SimplePhoto($storageManager, $dataStore);
```
