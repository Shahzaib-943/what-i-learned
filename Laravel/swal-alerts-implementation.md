
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

## Method 1 (Delete Confirmation) :

Step-1 : Paste the js and css links in your layout file (Step 1 of method 1).

Step-2 Make component for deletion, by command

```
php artisan make:component DeleteConfirmation
```

Step-3 : Pass id of item you want to delete.
Your compnent (app/View/Components/DeleteConfirmation.php), should look like this

```
<?php

namespace App\View\Components;

use Closure;
use Illuminate\Contracts\View\View;
use Illuminate\View\Component;

class DeleteConfirmation extends Component
{
    /**
     * Create a new component instance.
     */

     public $itemId;

    public function __construct($itemId)
    {
        $this->itemId = $itemId;
    }

    /**
     * Get the view / contents that represent the component.
     */
    public function render(): View|Closure|string
    {
        return view('components.delete-confirmation');
    }
}

```

Step-4 : In your blade make the delete button and call this component, like this

```
<a onclick="confirmDelete(event,{{ $quiz->id }})" href="{{ route('quiz.destroy', $quiz->id) }}" class="btn btn-danger">Delete <i class="fa-regular fa-trash-can"></i>
</a>

<x-delete-confirmation :item-id="$quiz->id" />
```
Step-5 : You view of component would look like this
```
<div>
    <script>
        function confirmDelete(event, itemId) {
            event.preventDefault();
            var urlToRedirect = event.currentTarget.getAttribute('href');
            Swal.fire({
                title: 'Are you sure?',
                text: "You won't be able to revert this!",
                icon: 'warning',
                showCancelButton: true,
                confirmButtonColor: '#d33',
                cancelButtonColor: '#3085d6',
                confirmButtonText: 'Yes, delete it!'
            }).then((result) => {
                if (result.isConfirmed) {
                    window.location.href = urlToRedirect;
                }
            });
        }
    </script>
</div>
```

You Confirmation Delte SWAL is good to go
## Author

- [@Shahzaib](https://github.com/Shahzaib-943)
