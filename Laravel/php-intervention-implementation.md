
# Implementing Laravel Intervention Image Package
By following this tutorial, you can easily install and implement the Intervention Image package, by which you can easily resize, edit,etc the images.

For this tutorial, we will resize the images and store them in different sizes.

[Official Documentation Link](https://image.intervention.io/v3)

Or visit the github repository
[Intervention Image](https://github.com/Intervention/image)




## Installation

Step-1 : Install the package via command:

```
composer require intervention/image
```
Step-2 : Install the GD PHP Extension via command:
```
sudo apt-get install php8.1-gd
```
## Example

We will use php intervention v3, and simply resize the images tht are widely used in websites.

Step 1 : Use these libraries in your controller.
```
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;
```

Step-2 : Just use driver to load images, example of controller is,

```
$fileDetailsArray = [];
$file = $request->file('file');
$originalName = $file->getClientOriginalName();
$fileSize = round($file->getSize()/1024 , 2);
$fileType = $file->getMimeType();
$extension = $file->getClientOriginalExtension();


$path = uploadFile($request->file);

$imagesSizes = ImageSizes::values();

$fileDetails = [
    'name' => $originalName,
    'url' => $path,
    'type' => $fileType,
    'extension' => $extension,
    'size' => $fileSize,
    'user_id' => Auth::user()->id
];

$fileCreated = Media::create( $fileDetails);

if(Str::startsWith($fileCreated->type, 'image'))
{
    $manager = new ImageManager(new Driver());
    $imagePath = public_path('storage/'.$fileCreated->url);
    $image = $manager->read($file);

    foreach(ImageSizes::map() as $size){
        list($width, $height) = explode('x', $size);
        $resizedImage = $image->resize($width, $height);
        $filenameWithoutExtension = pathinfo                                               ($fileCreated->name, PATHINFO_FILENAME);
        $newFilename = "{$filenameWithoutExtension}-{$size}.{$extension}";
        $folderPath = dirname($fileCreated->url);
        $resizedImage->save(public_path("storage/{$folderPath}/{$newFilename}"));
    }
}
```
Here we are simply calling all the ENUMS sizes and by foreach loop, we are resizing each image by placing the size in its name like (abc-240x240).







## Author

- [@Shahzaib](https://github.com/Shahzaib-943)
