# Guest Middleware & Groups

Now that we have protected routes like `/jobs/create` and `/jobs/edit/:id`, I now want to use the `Guest` middleware to make it so only guests or non-logged in users can access routes like `/login` and `/register`.

Open the `routes/web.php` file and add the following to the login route:

```php
Route::get('/login', [LoginController::class, 'login'])->name('login')->middleware('guest')->middleware('guest');
```

This is fine and we can add it to the register route as well. However, we can use a `group` to apply the middleware to multiple routes.

```php
Route::middleware('guest')->group(function () {
  Route::get('/register', [RegisterController::class, 'register'])->name('register');
  Route::post('/register', [RegisterController::class, 'store'])->name('register.store');
  Route::get('/login', [LoginController::class, 'login'])->name('login');
  Route::post('/login', [LoginController::class, 'authenticate'])->name('login.authenticate');
});
```

This is a bit cleaner. Now, only guests can access the login and register routes. If a user is logged in and tries to access these routes, they will be redirected to the home page.
