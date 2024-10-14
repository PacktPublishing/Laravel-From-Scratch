# User Avatar

I decided that I want to have users have the ability to upload an avatar. Right now, from the dashboard, we can see the user's name and email. I want to add an avatar to this as well. Let's add the avatar upload to the form.

## New Migration

We need to add a new column to the `users` table to store the avatar. Let's create a new migration for this.

```bash
php artisan make:migration add_avatar_to_users_table --table=users
```

Open the migration file and add the following code to the `up` method:

```php
Schema::table('users', function (Blueprint $table) {
    $table->string('avatar')->nullable()->after('email');
});
```

Add the following code to the `down` method:

```php
Schema::table('users', function (Blueprint $table) {
    $table->dropColumn('avatar');
});
```

Run the migration:

```bash
php artisan migrate
```

## Update User Model

Open the `app/Models/User.php` file and add the new field to the `$fillable` array:

```php
protected $fillable = [
    'name',
    'email',
    'password',
    'avatar',
];
```

## Update the Form

Open the `resources/views/dashboard/show.blade.php` file and add the following code right under the email field:

```html
<div class="mb-4">
  <label class="block text-gray-700" for="avatar">Profile Avatar</label>
  <input
    id="avatar"
    type="file"
    name="avatar"
    class="w-full px-4 py-2 border rounded focus:outline-none"
  />
</div>
```

## Avatar Preview

Let's add a preview of the avatar. Add the following right under the `h3` tag at the top of the page:

```html
@if($user->avatar)
<div class="mt-2 flex justify-center">
  <img
    src="{{ asset('storage/' . $user->avatar) }}"
    alt="Avatar"
    class="w-32 h-32 object-cover rounded-full"
  />
</div>
@endif
```

## Update the Profile Controller

Now open the `app/Http/Controllers/ProfileController.php` file and add the following code to the `update` method:

```php
 public function update(Request $request)
    {
        $user = Auth::user();

        // Validate the request
        $request->validate([
            'name' => 'required|string|max:255',
            'email' => 'required|email|max:255',
            'avatar' => 'nullable|image|mimes:jpeg,png,jpg,gif|max:2048',
        ]);

        // Update user details
        $user->name = $request->input('name');
        $user->email = $request->input('email');

        // Handle file upload
        if ($request->hasFile('avatar')) {
            // Delete old avatar if exists
            if ($user->avatar) {
                Storage::delete('public/' . $user->avatar);
            }

            // Store new avatar
            $avatarPath = $request->file('avatar')->store('avatars', 'public');
            $user->avatar = $avatarPath;
        }

        $user->save();

        return redirect()->route('dashboard.show')->with('success', 'Profile updated successfully.');
    }
```

Your file should be uploaded to `/storage/app/public/avatars` and should display in the preview. In the next lesson, let's show it in the navbar.
