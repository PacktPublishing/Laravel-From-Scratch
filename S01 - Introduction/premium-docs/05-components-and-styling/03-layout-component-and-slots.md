# Layout Components & Slots

As I said earlier, there are two ways to work with layouts. There is the template inheritance method, and there is the component method. We have already seen how to use the template inheritance method. In this lesson, we will learn how to use components for our layout and ultimately that is what we will use for our project.

Let's create a new Layout component. Run the following command to create a new component:

```bash
php artisan make:component Layout
```

Add the following to `resources/views/components/layout.blade.php`:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Workopia</title>
  </head>

  <body class="bg-gray-100">
    <x-header />
    <main class="container mx-auto p-4 mt-4">{{ $slot }}</main>
  </body>
</html>
```

The changes that we made are instead of `@yield`, we are using `{{ $slot }}`. The `$slot` variable is a special variable that contains the content of the child view. This is how we pass the content from the child view to the layout component. We can have multiple slots in a component by using named slots, but in this case, we only have one.

## Updating The Views

Now in order to use the layout component, we need to update both the `index.blade.php` and `create.blade.php` files.

Here is the new code for `index.blade.php`:

```html
<x-layout>
  <ul>
    @forelse($jobs as $job)
    <li>{{ $job }}</li>
    @empty
    <li>No jobs found</li>
    @endforelse
  </ul>
</x-layout>
```

We wrap everything in file with `<x-layout>`. This is cleaner than using `@extends` and `@section`.

Now update the `home.blade.php` and `create.blade.php` files with the following code respectively:

```html
<x-layout>
  <h1>Welcome to Workopia</h1>
  <p>Find your dream job today</p>
</x-layout>
```

```html
<x-layout>
  <x-slot name="title"> Create Job </x-slot>
  <h1>Create Job</h1>
  <form action="/jobs" method="POST">
    @csrf
    <input type="text" name="title" placeholder="Title" />
    <input type="text" name="description" placeholder="Description" />
    <button type="submit">Submit</button>
  </form>
</x-layout>
```

We do the same thing here. We wrap everything in the file with `<x-layout>`. We also set the title of the create page using the `<x-slot>` directive.

Now everything should work as before. You can test it by visiting the `/jobs` and `/jobs/create` routes.

From now on, we will use the component method for our layout. It is cleaner and more organized than the template inheritance method. Everything else as far as the controller and passing the data to the view remains the same.

You can delete the `layout.blade.php` file in the `views` folder with the template inheritance method. We won't be using it anymore.

## Move The Layout Component

If you want to move the layout component from the components folder to the views folder, you can. I am going to do that now. I am going to move the `layout.blade.php` file from `resources/views/components` to `resources/views/layouts`.

This will now break because it is looking in the components folder for the layout component. We can fix this by updating the `render` method in the `app/Views/Layout.php` file to the following:

```php
 public function render()
  {
    return view('layout');
  }
```

Now you can clear the view cache by running the following command:

```bash
php artisan view:clear
```

Now it should work as expected.

## Favicon

I have attached a download for a favicon that you can use for the project. You can download it from the resources section of this lesson. With Laravel, you simply add the file to the `public` folder and do a hard refresh of the browser to see the changes. Of course, if you want to use your own favicon, you can do that as well.



haha No problem at all. No time requirements to be a mod. That David guy is 100% insane. I had to block him. He used the code from my old PHP course as a base for Trongate. Which is fine. I said that's great. But then when I said I wouldn't promote it on my channel he acted like I stabbed him in the back. Very strange guy. Like seriously, I think he is mentally ill.