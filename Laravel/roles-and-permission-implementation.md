
# Implementing Spatie Roles and Permission
By following this tutorial, you can easily install and implement the roles and permissions through the spatie/laravel-permission package.

[Official Documentation Link](https://spatie.be/docs/laravel-permission/v6/introduction)





## Steps

Step-1 : Install the package via command:

```
composer require spatie/laravel-permission
```

Step-2 : Register the service provider in your config/app.php file:

```
'providers' => [
    // ...
    Spatie\Permission\PermissionServiceProvider::class,
];
```

Step-3 : Publish the migrations, by command

```
php artisan vendor:publish --provider="Spatie\Permission\PermissionServiceProvider"
```

Step-4 : Implement the trait in User model

```
// The User model requires this trait
 use HasRoles;
```

Step-5 : Run the migrations.

Step-6 : Make Seeders for roles, permissions and assigning permissions to roles.
For this tutorial, we will be making seeders for Quiz System

```
// Roles Seeder

$roles = [
            ['name' => 'admin' ],
            ['name' => 'user' ],
        ];

        foreach($roles as $role){
            Role::create($role);
        }

// Permission Seeder

$permissions = [
            ['name' => 'view quiz list'],
            ['name' => 'view quiz'],
            ['name' => 'attempt quiz'],
            ['name' => 'view quiz result'],
        ];

        foreach($permissions as $permission){
            Permission::create($permission);
        }

        $user = Role::where('name','user')->first();
        $user->givePermissionTo([
            'view quiz list',
            'view quiz',
            'attempt quiz',
            'view quiz result'
        ]);
```

Step-7 : Assign Role to the user in your RegisterController, as

```
protected function create(array $data)
    {
        $user =  User::create([
            'name' => $data['name'],
            'email' => $data['email'],
            'password' => Hash::make($data['password']),
        ]);

        $user->assignRole('user');

        return $user;
    }
```
NOTE : For the ADMIN,

Assign The role to the Admin in seeder.
```
$data = [
            'name' => 'Admin',
            'email' => 'admin@gmail.com',
            'password' => bcrypt('admin123')
        ];
        $user = User::create($data);
        $user->assignRole('admin');
```

And add the Before Gate in Providers/AuthServiceProvider's boot method to grant all permissions to the admin.
```
 public function boot(): void
    {
        Gate::before(function ($user, $ability) {
            return $user->hasRole('admin') ? true : null;
        });
    }

```





## Author

- [@Shahzaib](https://github.com/Shahzaib-943)

