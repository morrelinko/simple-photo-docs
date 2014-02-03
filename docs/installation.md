---
layout: default
title: Installation
---

### Requirements

* PHP 5.3+

This library can be installed through [Composer](http://getcomposer.org)  [Recommended]

{% highlight json %}
{
    "require": {
        "morrelinko/simple-photo": "2.1.0"
    }
}
{% endhighlight %}

Or manually by loading the *autoloader* that came with simple-photo

{% highlight php %}
require_once '/path/to/simple-photo/autoload.php';
{% endhighlight %}

Note: This library depends on the [Imagine](https://packagist.org/packages/imagine/imagine)
library for image transformation
