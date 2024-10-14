# Layouts Using Template Inheritance

Right now, we have a couple views. We have a `jobs/index.blade.php` view and a `jobs/create.blade.php` view. Notice that both of these files have the HTML boilerplate with the `head` and `body` tags. If we have to add this boilerplate to every view, it will be a lot of duplication. This is where layouts come in.

A layout is a template that we can use to wrap around our views. We can define a layout that contains the HTML boilerplate and then include our views inside the layout. This way, we can avoid duplicating the boilerplate code in every view.

There are a few ways to use layouts. We can do it the traditional way using template Inheritance as well as using layouts using components, which is the more modern way. We're going to be using components, however I want to show you both ways because you probably will run into the old way using template inheritance and partials. Let's start with the that.

## Create A Layout

Let's create a layout that we can use to wrap around our views. Create a file at `resources/views/layout.blade.php` and add the following code:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Workopia | Find and list jobs</title>
  </head>

  <body class="bg-gray-100">
    <h1>My App</h1>
    <main class="container mx-auto p-4 mt-4">@yield('content')</main>
  </body>
</html>
```

The `@yield` directive is used to define a section that can be overridden by a child view. We will use this directive to include our view content inside the layout. I just put the `<h1>` there in the body so that you can see that this will show on every page that uses this layout. I also added some classes to the `body` and `main` tags for styling.

## Use The Layout

Now that we have a layout, let's use it in our views. Open the `jobs/index.blade.php` file and replace the content with the following code:

```html
@extends('layout') @section('content')
<h1>{{ $title }}</h1>

@forelse($jobs as $job)
<li>{{ $job }}</li>
@empty
<li>No Jobs Found</li>
@endforelse @endsection
```

Here, we are using the `@extends` directive to extend the layout. The argument we are passing in is the location and name of the layout relative to the views folder. If we had it in `resources/views/layouts/app.blade.php`, we would pass in `layouts.app`.

We are also using the `@section` directive to define the content that will be included in the layout. The `@section` directive takes a name as an argument. In this case, we are using the name `content`. That is what we passed into the main `@yield` directive in the layout.

## Add Layout To Other Views

Do the same for the `pages/home.blade.php` file:

```html
@extends('layout') @section('content')
<h1>Welcome to Workopia</h1>
<p>Find your dream job today</p>
@endsection
```

Do the same for the `jobs/create.blade.php` file:

```html
@extends('layout') @section('content')
<h1>Create Job</h1>
<form action="/jobs" method="POST">
  @csrf
  <input type="text" name="title" placeholder="Title" />
  <input type="text" name="description" placeholder="Description" />
  <button type="submit">Submit</button>
</form>
@endsection
```

You should see the `<h1>My App</h1>` tag on all 3 pages. This is because we are extending the layout and defining the content that will be included in the layout using the `@section` directive. You can delete that `<h1>` tag from the layout now.

## Title Section

Let's add another `@yield` directive for the title in the layout. Open the `layout.blade.php` file and update it like this:

```html
<title>@yield('title', 'Workopia | Find or List a Job')</title>
```

Here we are using the `@yield` directive to define a default title for the layout. If a child view does not override this section, the default title will be used.

I want to use the default for `jobs/index.blade.php`, so we won't add a title section there, but for `jobs/create.blade.php`, add the following above the content section:

```php
@section('title')
Create Job
@endsection
```

Now the title should change to `Create Job` when you visit the `/jobs/create` route.
