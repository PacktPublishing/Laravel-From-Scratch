# User Authentication

Now that we can register a user, let's add log in functionality. We already have our `LoginController` and view. Let's add the form to the view.

Open the `resources/views/auth/login.blade.php` file and add the following code:

```html
<x-layout>
  <div
    class="bg-white rounded-lg shadow-md w-full md:max-w-xl mx-auto mt-12 p-8 py-12"
  >
    <h2 class="text-4xl text-center font-bold mb-4">Login</h2>
    <form method="POST" action="{{ route('login.authenticate') }}">
      @csrf
      <x-inputs.text
        id="email"
        name="email"
        type="email"
        placeholder="Email address"
      />
      <x-inputs.text
        id="password"
        name="password"
        type="password"
        placeholder="Password"
      />
      <button
        type="submit"
        class="w-full bg-blue-500 hover:bg-blue-600 text-white px-4 py-2 rounded focus:outline-none"
      >
        Login
      </button>

      <p class="mt-4 text-gray-500">
        Don't have an account?
        <a class="text-blue-900" href="{{route('register')}}">Register</a>
      </p>
    </form>
  </div>
</x-layout>
```

This is very similar to the registration form we created earlier. The only difference is we don't have a name or confirm password fields. And obviously it is being submitted to a different route.

You should be able to go to `http://localhost:8000/login` and see the login page.

## `authenticate` Method

Now let's handle the `authenticate` method in our `LoginController`. Open the `app/Http/Controllers/LoginController.php` file and add the following imports:

```php
use Illuminate\Support\Facades\Auth;
```

#### Validate the Request Data

Add the following code to the method:

```php
 public function authenticate(Request $request): RedirectResponse
{
    // Validate the request data
    $credentials = $request->validate([
        'email' => 'required|email',
        'password' => 'required|string',
    ]);

    dd($credentials);
}
```

You should see the credentials in the browser whether they are valid or not. Now we need to test if the credentials are valid.

#### Authenticate the User

Add the following code to the method:

```php
 // Attempt to log the user in
if (Auth::attempt($credentials)) {
    // Regenerate the session to prevent fixation attacks
    $request->session()->regenerate();

    // Redirect to the intended route or a default route
    return redirect()->intended(route('home'))->with('success', 'You are now logged in!');
}
```

This code will attempt to log in with the specified credentials. If the credentials are valid, it will log in the user and redirect them to the intended route or a default route.

The `regenerate()` method is used to regenerate the session to prevent fixation attacks. This is a security measure to prevent attackers from hijacking a user's session.

You should now be able to log in with the credentials you used to register. If you are not able to log in, check the credentials you used to register. If you are still having trouble, check the `User` model to make sure the password is being hashed.

When you log in, you will be redirected with a message. Check your `sessions` table and you should see an entry with `user_id` filled with your ID.

#### On Failure

If the credentials fail, we will redirect back with a message. Add this below the if statement you just wrote:

```php
 // If authentication fails, redirect back with an error message
        return back()->withErrors([
            'email' => 'The provided credentials do not match our records.',
        ])->onlyInput('email');
```

Next, we need to be able to log out. Let's add that functionality next.
