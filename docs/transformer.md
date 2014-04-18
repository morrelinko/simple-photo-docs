---
layout: docs
title: Transformer
---

Transformers are classes that are called upon when the `'transform'` option is defined

either during upload or when retrieving photos.

SimplePhoto comes shipped with a `DefaultTransformer` that only implements basic

transformation options such as 'resize' && 'rotate'. If these are the only photo transformations your app

requires, then you are good to go. But, if you want more, adding yours is easy.

First, create your transformation class implementing the `SimplePhoto\Transformer\TransformerInterface`

```php
<?php
use SimplePhoto\Transformer\TransformerInterface;

class TransformerOnSteroids implements TransformerInterface
{
    /**
     * @param string $file The Image File
     * @param array $transformOptions The array of transformations to be performed
     * @param array $parameters Some extra parameters passed on from simple photo
     */
    public function transform($file, array $transformOptions = array(), array $parameters = array())
    {
        $image = $imageHandler->load($file);

        if (isset($transformOptions['resize'])) {
            // Code to resize
            list($width, $height) = $transformOptions['resize'];
            $image->applyResize($width, $height);
        } else if (isset($transformOptions['grayscale'])) {
            // Code to apply grayscale to image
            $image->applyGrayscaleEffect();
        }

        .....
    }

    /**
     * Used to generate a string that will be appended to the photo file name
     * after performing some transformations on the original photo.
     */
    public function generateName(array $transformOptions = array())
    {
        $suffix = '';
        if (isset($transformOptions['resize'])) {
            list($width, $height) = $transformOptions['resize'];
            $suffix .= 'resize' . $width . 'x' . $height;
        } else if (isset($transformOptions['grayscale'])) {
            $suffix .= 'grscale';
        }

        return $suffix;
    }
}
```

Next tell `SimplePhoto` to use your transformer instead of the default transformer

```php
<?php

$simplePhoto->setTransformer(new TransformerOnSteroids());
```

That's it... You can now do.

```php
<?php

$simplePhoto->get($id, [
    'transform' => [
        'grayscale' => true
    ]
]);
```