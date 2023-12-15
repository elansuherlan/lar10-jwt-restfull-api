### Step 1: Install Laravel
Do this command if you want to install on current directory without create new directory:
```
composer create-project laravel/laravel .
```
If you want to create with new directory, do this command:
```
composer create-project laravel/laravel {your_directory}
```
### Step 2: Install JWT (JSON Web Token)
```
composer require tymon/jwt-auth
```
### Step 3: Open app.php file from /config folder
- Add this code into "providers"
  ```
  Tymon\JWTAuth\Providers\LaravelServiceProvider::class,
  ```
- Add this code into "aliases"
  ```
  'Jwt' => Tymon\JWTAuth\Providers\LaravelServiceProvider::class,
  'JWTFactory' => Tymon\JWTAuth\Facades\JWTFactory::class,
  'JWTAuth' => Tymon\JWTAuth\Facades\JWTAuth::class,
  ```
### Step 4: Publish jwt.php
```
php artisan vendor:publish --provider="Tymon\JWTAuth\Providers\LaravelServiceProvider"
```
It will copy a file **jwt.php** inside **/config folder**.
### Step 5: Run Migration
```
php artisan migrate
```
It will migrate all pending migrations of application.
### Step 6: Generate JWT Secret Token
```
php artisan jwt:secret
```
It updates **.env** file with jwt secret key.
### Step 7: Update Model User.php
Open **User.php** file from **/app/Models** folder.
```
use Tymon\JWTAuth\Contracts\JWTSubject;
```
Add this code inside User class
```
public function getJWTIdentifier()
{
  return $this->getKey();
}

public function getJWTCustomClaims()
{
  return [];
}
```
### Step 8: Create ApiController.php
```
php artisan make:controller Api/ApiController
```
It will create a file named **ApiController.php** inside **/app/Http/Controllers** folder.
