
# Implementing Toastr Alerts
If you want to add the beautiful toastr allerts, you can easily add them by following the steps.
There are two ways or methods to implement them.

## Method 1 (By cdn links) : 



### Installation

Step-1 : Paste the js and css links in your layout file.

```bash
<link href="https://cdnjs.cloudflare.com/ajax/libs/toastr.js/latest/toastr.min.css" rel="stylesheet">
    
<script src="https://cdnjs.cloudflare.com/ajax/libs/toastr.js/latest/js/toastr.min.js"></script>
```


Step-2 : Make a new component for alerts.

```bash
php artisan make:component alert --view
```
" --view flag will only make the blade named as "resources/views/components/alert.blade.php" "


Step-3 : Flash the alerts in your livewire component or controller.
```bash
session()->flash('alert', ['message' => 'Post successfully created','type' => 'success']);
```
" session->flash() will store the key-value pairs only for the next HTTP request, its useful for showing the redirect messages "

Step-4 : Write the script for your alert in "alert.blade.php" file
```bash
<div>
    @if(Session::has('alert'))
        <script>
            toastr.options = 
            {
                "closeButton": true,                    
                "progressBar": true
            }

            var messageType = "{{ session('alert')['type'] ?? 'success' }}";
            var messageText = "{{ session('alert')['message'] }}";

            toastr[messageType](messageText);
        </script>
    @endif
</div>
```

Step-5 : In your layout or desired blade file, add the component.
```bash
    <x-alert />
```
You are good to go for method 1....


## Author

- [@Shahzaib](https://github.com/Shahzaib-943)

