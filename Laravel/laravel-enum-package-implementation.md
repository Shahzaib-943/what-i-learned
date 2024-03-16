
# Implementing Laravel ENUM Package

This tutorial implements the larvel enum package. It is laravel package that introduces a new Artisan command to generate Enum classes.


In this tutorial, we will make the enum class for different sizes of the images usually used in the website. Then later we can call this class when resizing the images.



Visit the github repository
[Intervention Image](https://github.com/cerbero90/laravel-enum)




## Installation

Step-1 : Install the package via command:

```
composer require cerbero/laravel-enum
```
Thats it, this package is intalled.

## Example

We will make the enum class for different sizes of the images usually used in the website. 

Step-1 : Run the command to make the enum class.
```
php artisan make:enum ImageSizes 'SIZE_150x150|SIZE_240x240|SIZE_300x188|SIZE_525x328
|SIZE_580x363|SIZE_768x480|SIZE_1024x680|SIZE_1536x690'
```
This will make a class in app\Enums\ImageSizes, that will look like this
```
<?php

namespace App\Enums;

use Rexlabs\Enum\Enum;

/**
 * The ImageSizeas enum.
 *
 * @method static self SIZE_150x150()
 * @method static self SIZE_240x240()
 * @method static self SIZE_300x188()
 * @method static self SIZE_525x328()
 * @method static self SIZE_580x363()
 * @method static self SIZE_768x480()
 * @method static self SIZE_1024x680()
 * @method static self SIZE_1536x690()
 */
class ImageSizes extends Enum
{
    const SIZE_150x150 = 'size_150x150';
    const SIZE_240x240 = 'size_240x240';
    const SIZE_300x188 = 'size_300x188';
    const SIZE_525x328 = 'size_525x328';
    const SIZE_580x363 = 'size_580x363';
    const SIZE_768x480 = 'size_768x480';
    const SIZE_1024x680 = 'size_1024x680';
    const SIZE_1536x690 = 'size_1536x690';
}
```

Step 2 : Make a map function to return the values,so we can use them in our controller. Like this
```
<?php

namespace App\Enums;

use Rexlabs\Enum\Enum;

/**
 * The ImageSizes enum.
 *
 * @method static self SIZE_150x150()
 * @method static self SIZE_240x240()
 * @method static self SIZE_300x188()
 * @method static self SIZE_525x328()
 * @method static self SIZE_580x363()
 * @method static self SIZE_768x480()
 * @method static self SIZE_1024x680()
 * @method static self SIZE_1536x690()
 */
class ImageSizes extends Enum
{
    const SIZE_150x150 = 'size_150x150';
    const SIZE_240x240 = 'size_240x240';
    const SIZE_300x188 = 'size_300x188';
    const SIZE_525x328 = 'size_525x328';
    const SIZE_580x363 = 'size_580x363';
    const SIZE_768x480 = 'size_768x480';
    const SIZE_1024x680 = 'size_1024x680';
    const SIZE_1536x690 = 'size_1536x690';

    public static function map(): array
    {
        return [
            static::SIZE_150x150 => '150x150',
            static::SIZE_240x240 => '240x240',
            static::SIZE_300x188 => '300x188',
            static::SIZE_525x328 => '525x328',
            static::SIZE_580x363 => '580x363',
            static::SIZE_768x480 => '768x480',
            static::SIZE_1024x680 => '1024x680',
            static::SIZE_1536x690 => '1536x690',
        ];
    }
}
```
That's it, now we can call the values in our controller, simly by
```
$imagesSizes = ImageSizes::values();
```
Now if we do, dd($imagesSizes), it will dump these values.
```
array:8 [ // app/Http/Controllers/MediaController.php:74
  0 => "150x150"
  1 => "240x240"
  2 => "300x188"
  3 => "525x328"
  4 => "580x363"
  5 => "768x480"
  6 => "1024x680"
  7 => "1536x690"
]
``` 

Now we have created the ENUM class, successfully.


## Author

- [@Shahzaib](https://github.com/Shahzaib-943)
