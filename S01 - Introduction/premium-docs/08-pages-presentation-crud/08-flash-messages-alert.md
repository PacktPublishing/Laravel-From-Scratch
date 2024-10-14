# Alert Components

In this lesson, I want to handle the success or error messages in the session when we redirect with an alert component.

Make sure in the `JobController` you have the following in the `store` method:

```php
return redirect()->route('jobs.index')->with('success', 'Job listing created successfully!');
```

Create a new component called `Alert`. Run the following command:

```bash
php artisan make:component Alert
```

Open the `resources/views/components/Alert.blade.php` file and add the following code:

```php
@props(['type', 'message'])

@if(session()->has('success') || session()->has('error'))
<div class="p-4 mb-4 text-sm text-white {{ $type === 'success' ? 'bg-green-500' : 'bg-red-500' }} rounded">
    {{ $message }}
</div>
@endif
```

Let's add the component to the layout. Open the `resources/views/components/layout.blade.php` file and add the following code above the `{{ $slot }}`:

```php
 <!-- Display alert messages -->
  @if (session('success'))
  <x-alert type="success" message="{{ session('success') }}" />
  @endif

  @if (session('error'))
  <x-alert type="error" message="{{ session('error') }}" />
  @endif
```

Now submit a new job listing and you should see the success message.

One issue we have that I don't like is that the message stays there until we refresh the page. We can change that with a little JavaScript. For interactive stuff like this in Laravel, I like to use Alpine.js. We will do that in the next lesson.
