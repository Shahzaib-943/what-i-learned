
# Making View Composer

Often, we need a certain type of data to be available on multiple pages. Typical way is to execute queries to fetch data and pass this data to multple views in controller. A better way to do this to make view composer and pass the data to array of views.

In this tutorial, we will make a composer view to pass certain data to a modal component, which we'll be calling on multiple pages.


## Implementation

Step-1 : Make a service provider class by fllowing command:

```
php artisan make:provider ViewServiceProvider
```

Step-2 : Register the newly created service provider class in config/app.php in providers key, like this:

```
'providers' => ServiceProvider::defaultProviders()->merge([
        
        App\Providers\AuthServiceProvider::class,
        // 
        App\Providers\ViewServiceProvider::class,
    ])->toArray(),
```

Step-3 : Now in service provider class, inside boot method pass view array and callback function or in my case, composer class. like this.

```
public function boot(): void
{
    View::composer('components.media-modal', MediaModalComposer::class);  
}
```

Step-4 : Now make a new composer file manually in app\View\Composers\MediaModalComposer (Best Practise, not restricted) and inside it, make compose method and pass the required data like this, 

```
<?php

namespace App\View\Composers;

use App\Models\Media;
use Illuminate\View\View;
use App\Repositories\UserRepository;

class MediaModalComposer
{
    public function compose(View $view): void
    {
        $files = Media::with('user:id,name')->get();
        $fileTypes = $files->pluck('extension')->unique();
        $dates = Media::orderBy('created_at')->pluck('created_at')->unique()->map(function ($date) {
            return \Carbon\Carbon::parse($date)->format('F - Y');
        })->unique();
        $modalOpenedFlag = false;

        $view->with(['files' => $files, 'fileTypes' => $fileTypes, 'dates' => $dates, 'modalOpenedFlag' => $modalOpenedFlag]);
    }
}

```



Thats it, now we can call the component or view, where ever we want, without pasing data variables.

```
<x-media-modal/>
```







## Author

- [@Shahzaib](https://github.com/Shahzaib-943)
