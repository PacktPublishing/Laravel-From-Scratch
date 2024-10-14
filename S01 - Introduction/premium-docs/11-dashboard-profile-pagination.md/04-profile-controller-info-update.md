# Profile Controller & Update User Info

We need to add a form on the dashboard page that shows the user's info and we want to be able to update that info. I am going to create a separate controller for this because it relates more to the user "profile".

Let's open the `/resources/views/dashboard/index.blade.php`. I want the profile form and the listings to be side by side. So add this at the very top just after the opening `<x-layout>`:

  ```html
   <section class="flex flex-col md:flex-row gap-6">
  ```

At the bottom, close it just above the closing `</x-layout>`. I am also going to show the bottom banner component on the dashboard:

```html
  </section>
  <x-bottom-banner />
</x-layout>
```

Now we need to add the following above the job listings div:

```html
 <div class="bg-white p-8 rounded-lg shadow-md w-full md:w-1/2">
  <h3 class="text-3xl text-center font-bold mb-4">Profile Info</h3>
  <form method="POST" action="{{ route('profile.update') }}" enctype="multipart/form-data">
    @csrf
    @method('PUT')

    <div class="mb-4">
      <label class="block text-gray-700" for="name">Name</label>
      <input id="name" type="text" name="name" value="{{ $user->name }}"
        class="w-full px-4 py-2 border rounded focus:outline-none" />
    </div>
    <div class="mb-4">
      <label class="block text-gray-700" for="email">Email</label>
      <input id="email" type="text" name="email" value="{{ $user->email }}"
        class="w-full px-4 py-2 border rounded focus:outline-none" />
    </div>
    <div class="mb-4">
      <label class="block text-gray-700" for="avatar">Profile Avatar</label>
      <input id="avatar" type="file" name="avatar" class="w-full px-4 py-2 border rounded focus:outline-none" />
    </div>
    <button type="submit"
      class="w-full bg-green-500 hover:bg-green-600 text-white px-4 py-2 my-3 rounded focus:outline-none">Save</button>
  </form>
</div>
```

## Profile Controller

Let's create a new profile controller:

```bash
php artisan make:controller ProfileController
```

Open the controller and add the import for the user model:

```php
use App\Models\User;
```

Next, let's add the `update` method to the `ProfileController`:

```php
public function update(Request $request): RedirectResponse
{
    // Get the authenticated user
    $user = Auth::user();

    // Validate the incoming request data
    $validatedData = $request->validate([
        'name' => 'required|string|max:255',
        'email' => 'required|string|email|max:255|unique:users,email,' . $user->id,
    ]);

    // Update the user's information
    $user->update($validatedData);

    // Redirect back to the dashboard page with a success message
    return redirect()->route('dashboard.show')->with('success', 'User info updated successfully!');
}
```

Be sure to import the `RedirectResponse` class at the top of the file:

```php
use Illuminate\Http\RedirectResponse;
```

This is pretty self-explanatory. We are validating the incoming request data, updating the user's information, and then redirecting back to the profile page with a success message.

The reason we pass the `$user->id` to the `email` validation rule is to make sure that the email is unique, except for the current user. This is because we don't want to allow the user to change their email to one that already exists in the database.

## Add Update Route


You need to create the update route. Open the `routes/web.php` file and add the following import:

```php
use App\Http\Controllers\ProfileController;
```

Now add the route:

```php
Route::put('/profile', [ProfileController::class, 'update'])->name('profile.update')->middleware('auth');
```

Now you should be able to update your name and email and it should show in the dashboard.
