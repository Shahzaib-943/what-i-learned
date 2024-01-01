
# Implementing Custom Mails
If you want to send custom emails to the users,implement them easily by following the steps.

We will be sending thanks mail to the doctor that registered in our application

### Requirements : 

- Email credentials ready.
- Configure the .env file with mail credentials.





### Installation

Step-1 : Make a new Email by following command.

```bash
php artisan make:mail DoctorThanksMail
```


Step-2 : Make the view for email to be send.

Step-3 : In the controller, mention the mail class, which we created in step 1(DoctorThanksMail).

```bash
$name = $vendor->f_name.' '.$vendor->l_name;

try
{
    $mail = Mail::to($vendor->email)->send(new DoctorThanksMail($name));
}
catch (\Exception $e)
{
    return response()->json([
        'success' => false,
        'message' => "Email sending error: " . $e->getMessage()
    ]);
}
```

Step-4 : In the mail class DoctorThanksMail, pass the values which we passed in the blade file, to the constructor
```bash
public $name;
    
public function __construct($name)
{
    $this->name = $name;
}
    
public function build()
{
    return $this->view('email-templates.doctor-thank')->subject('Thank You For Submitting The Application');
}
```


You are good to go ...


## Author

- [@Shahzaib](https://github.com/Shahzaib-943)

