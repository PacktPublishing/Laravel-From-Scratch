# Log Out User & Auth Directive

Now that we are logged in, we need a way to log out. I also want to show and hide links based on the user's authentication status. We can use the `@auth` directive to do this.

## Logout Route

Let's add a new route to the `routes/web.php` file:

```php
Route::post('/logout', [LoginController::class, 'logout'])->name('logout');
```

## `logout` Method

Next, let's add a `logout` method to the `LoginController` class:

```php
public function logout(Request $request): RedirectResponse
{
    Auth::logout(); // Log out the user

    $request->session()->invalidate(); // Invalidate the session
    $request->session()->regenerateToken(); // Regenerate the CSRF token

    return redirect('/');
}
```

## Logout Button & `@auth` Directive

Finally, let's add a logout button to the layout file. Open the `resources/views/components/header.blade.php` file and replace all the code with the following:

```html
<header class="bg-blue-900 text-white p-4" x-data="{ open: false }">
  <div class="container mx-auto flex justify-between items-center">
    <h1 class="text-3xl font-semibold">
      <a href="{{ route('home') }}">Workopia</a>
    </h1>
    <nav class="hidden md:flex items-center space-x-4">
      <x-nav-link url="/" :active="request()->is('/')">Home</x-nav-link>
      <x-nav-link url="/jobs" :active="request()->is('jobs')"
        >All Jobs</x-nav-link
      >
      @auth
      <x-nav-link url="/jobs/saved" :active="request()->is('jobs/saved')"
        >Saved Jobs</x-nav-link
      >
      <x-nav-link
        url="/dashboard"
        :active="request()->is('dashboard')"
        icon="gauge"
        >Dashboard</x-nav-link
      >
      <form method="POST" action="{{ route('logout') }}">
        @csrf
        <button type="submit" class="text-white">
          <i class="fa fa-sign-out"></i> Logout
        </button>
      </form>
      <x-button-link url="/jobs/create" type="button" icon="edit"
        >Create Job</x-button-link
      >
      @else
      <x-nav-link url="/login" :active="request()->is('login')"
        >Login</x-nav-link
      >
      <x-nav-link url="/register" :active="request()->is('register')"
        >Register</x-nav-link
      >
      @endauth
    </nav>
    <button
      @click="open = !open"
      class="text-white md:hidden flex items-center"
    >
      <i class="fa fa-bars text-2xl"></i>
    </button>
  </div>
  <!-- Mobile Menu -->
  <nav
    x-show="open"
    @click.away="open = false"
    class="md:hidden bg-blue-900 text-white mt-5 pb-4 space-y-2"
  >
    <x-mobile-nav-link url="/" :active="request()->is('/')"
      >Home</x-mobile-nav-link
    >
    <x-mobile-nav-link url="/jobs" :active="request()->is('jobs')"
      >All Jobs</x-mobile-nav-link
    >
    @auth
    <x-mobile-nav-link url="/jobs/saved" :active="request()->is('jobs/saved')"
      >Saved Jobs</x-mobile-nav-link
    >
    <x-mobile-nav-link
      url="/dashboard"
      :active="request()->is('dashboard')"
      icon="gauge"
      >Dashboard</x-mobile-nav-link
    >
    <form method="POST" action="{{ route('logout') }}">
      @csrf
      <button type="submit" class="text-white">
        <i class="fa fa-sign-out"></i> Logout
      </button>
    </form>
    <div class="py-2">
      <x-button-link url="/jobs/create" type="button" icon="edit"
        >Create Job</x-button-link
      >
    </div>
    @else
    <x-mobile-nav-link url="/login" :active="request()->is('login')"
      >Login</x-mobile-nav-link
    >
    <x-mobile-nav-link url="/register" :active="request()->is('register')"
      >Register</x-mobile-nav-link
    >
    @endauth
  </nav>
</header>
```

You will only see certain links if you are logged in or logged out. The logout button will kill the session and redirect you to the home page.

## Authenticate On Register

One more thing I want to do when it comes to our authentication system is to authenticate the user right after they register.

Open the `RegisterController` class and add the following import:

```php
use Illuminate\Support\Facades\Auth;
```

Then in the `store` method, add the following line right above the `return redirect()->route('home')` line:

```php
Auth::login($user);
```

Now the user will be logged in after they register.
