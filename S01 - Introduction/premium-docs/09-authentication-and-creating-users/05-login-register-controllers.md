# Login & Register Controllers

We are going to build a custom login using some of the tools that Laravel offers. We even have the tables already created for us. We have a users table from the default migration files that come with Laravel. We also have a `User` model that is already setup for us.

## Create Controllers

When it comes to structure, there are many ways that you can handle authentication. A common approach is to create a controller for each type of authentication. For example, you might have a `LoginController` and a `RegisterController`. This allows you to keep your code organized and easy to maintain.

Let's create two new controllers:

```bash
php artisan make:controller LoginController
php artisan make:controller RegisterController
```

This will create two new files in the `app/Http/Controllers` directory. You can find them at `app/Http/Controllers/LoginController.php` and `app/Http/Controllers/RegisterController.php`.

## Create Routes

Next, we need to create routes for our new controllers. Open the `routes/web.php` file.

We need to import the `LoginController` and `RegisterController` classes. Add the following to the top of the file.

```php
use App\Http\Controllers\RegisterController;
use App\Http\Controllers\LoginController;
```

Then add the following routes.

```php
Route::get('/register', [RegisterController::class, 'register']);
Route::post('/register', [RegisterController::class, 'store']);
Route::get('/login', [LoginController::class, 'login']);
Route::post('/login', [LoginController::class, 'authenticate']);
```

The first route is for the registration form. The second route is for the registration form submission. The third route is for the login form. The fourth route is for the login form submission.

#### Naming Routes

You can also apply a name to the routes. This is useful for generating URLs.

Let's give all of the routes a name except for the resource routes.

```php
Route::get('/', [HomeController::class, 'index'])->name('home');
Route::get('/jobs/{id}/save', [JobController::class, 'save'])->name('jobs.save');
Route::resource('jobs', JobController::class);
Route::get('/register', [RegisterController::class, 'register'])->name('register');
Route::post('/register', [RegisterController::class, 'store'])->name('register.store');
Route::get('/login', [LoginController::class, 'login'])->name('login');
Route::post('/login', [LoginController::class, 'authenticate'])->name('login.authenticate');
```

## Register Controller

Let's start with the `RegisterController`. Add the following imports for the types:

```php
use Illuminate\View\View;
use Illuminate\Http\RedirectResponse;
```

We will create a `register` method that will return the registration form. We will also create a `store` method that will handle the registration form submission.

Let's start with the `register` method.

```php
// @desc  Show register form
// @route GET /register
public function register(): View {
  return view('auth.register');
}
```

For now we will just create the view with a a heading or something. Create a folder called `auth` in the `resources/views` folder. Inside the `auth` folder create a file called `register.blade.php`.

```html
<x-layout>
  <h1>Register</h1>
</x-layout>
```

Now you should be able to go to `http://localhost:8000/register` and see the heading.

Let's also create a method called `store` that will handle the registration form submission. For now, we will just return a string.

```php
// @desc  Store new user
// @route POST /register
public function store(): string {
  return 'store';
}
```

We will come back to that later.

## Login Controller

Let's add to the LoginController. Add the following imports for the types:

```php
use Illuminate\View\View;
use Illuminate\Http\RedirectResponse;
```

We are going to create a few methods in the `LoginController`. We will create a `login` method that will return the login form. We will also create an `authenticate` method that will handle the login form submission.

Let's start with the `login` method.

```php
// @desc  Show login form
// @route GET /login
public function login(): View {
  return view('auth.login');
}
```

In the `/resources/views/auth` folder, create a file called `login.blade.php` and add the following for now:

```html
<x-layout>
  <h1>Login</h1>
</x-layout>
```

Now you should be able to go to `http://localhost:8000/login` and see the heading.

Create the `authenticate` method.

```php
// @desc  Log in user
// @route POST /authenticate
public function authenticate(Request $request): string {
  return 'authenticate';
}
```

We will come back to that later.
