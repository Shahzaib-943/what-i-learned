
# SweetAlerts (swal) Alerts Implementation
If you want to add the beautiful sweet alerts, you can easily add them by following the steps.
There are two ways or methods to implement them.

## Method 1 (By cdn links) : 



### Installation

Step-1 : Paste the js and css links in your layout file.

```bash
<script src="https://cdn.jsdelivr.net/npm/sweetalert2@10.16.6/dist/sweetalert2.all.min.js"></script>

<link rel='stylesheet' href='https://cdn.jsdelivr.net/npm/sweetalert2@10.10.1/dist/sweetalert2.min.css'>
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
            var messageType = "{{ session('alert')['type'] ?? 'success' }}";
            var messageText = "{{ session('alert')['message'] }}";

            Swal.fire(
                messageText,
                '',
                messageType
                )
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

