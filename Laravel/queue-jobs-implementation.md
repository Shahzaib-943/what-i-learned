
# Implementing Queue Jobs
If you want to implement the queue jobs in laravel, you can do it easily by following this tutoril.

For this tutorial, we are implementing queue for sending the emails.





## Steps

Step-1 : Make a new mail class by following command
```
php artisan make:mail sendFamilyIdToIndependentUser
```

Step-2 : Change the environment variable "QUEUE_DRIVER".

```bash
QUEUE_DRIVER=database
```


Step-3 : Make a table for queue jobs, by creating and running the following migration.

```bash
php artisan queue:table
```
then
```
php artisan migrate
```
_It will make a table named as "jobs" in the DB._


Step-4 : Make a queue job by following command.
```bash
php artisan make:job sendFamilyIdToIndependentUserJob
```
_It will make a new file in app/Jobs/sendFamilyIdToIndependentUserJob_



Step-5 : Import the Email Class made and Mail, like this
```bash
use App\Mail\sendFamilyIdToIndependentUser;
use Mail;
```

Step-5 : In handle function of queue job, write all the logic.
```bash
    public function handle()
    {
        Mail::to($this->email)->send(new sendFamilyIdToIndependentUser(
            $this->name, $this->email, $this->familyId
        ));
    }
```
Step-6 : If you are implementing it in local server, check queue jobs by command.
```bash
   php artisan queue:work
```
If you want to run queues on live server, run the command and it will make the file "queue.log" file in root folder of your poject.
```
nohup php artisan queue:listen --timeout=3000 > /home/s3bitsdev/public_html/ddf/queue.log 2>&1 &
tail -f /home/s3bitsdev/public_html/ddf/queue.log
```
Here  paste your project's path instead of "/home/s3bitsdev/public_html/ddf/queue.log"
You can find the path by moving ti the root of your project and running the following command
```
pwd
```
You are good to go ....


## Author

- [@Shahzaib](https://github.com/Shahzaib-943)

