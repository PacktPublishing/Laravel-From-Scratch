# Search Component & Route

We have a hero component now that has a form in it. I want to make that form a search component that can be reused in other parts of the application. 

Let's create the component:

```bash
php artisan make:component Search
```

Open the `/resources/views/components/search.blade.php` and copy the form from the hero and paste it in the new file.

```html
<form class="block mx-5 md:mx-auto md:space-x-2">
  <input
    type="text"
    name="keywords"
    placeholder="Keywords"
    class="w-full md:w-72 px-4 py-3 focus:outline-none"
  />
  <input
    type="text"
    name="location"
    placeholder="Location"
    class="w-full md:w-72 px-4 py-3 focus:outline-none"
  />
  <button
    class="w-full md:w-auto bg-blue-700 hover:bg-blue-600 text-white px-4 py-3 focus:outline-none"
  >
    <i class="fa fa-search mr-1"></i> Search
  </button>
</form>
```

Then in the hero component, replace the form with the search component.

```html
@props(['title' => 'Find Your Dream Job'])
<section
  class="hero relative bg-cover bg-center bg-no-repeat h-80 flex items-center "
>
  <div class="overlay"></div>
  <div class="container mx-auto text-center z-10">
    <h2 class="text-4xl md:text-5xl text-white font-bold mb-8">{{ $title }}</h2>
    <x-search />
  </div>
</section>
```

I also want the search on the /jobs page. Open the `resources/views/jobs/index.blade.php` file and add the search component and a wrapper div at the top of the page as the first element in the `<x-layout>` component.

```html
<div
  class="bg-blue-900 h-24 px-4 mb-4 flex justify-center items-center rounded"
>
  <x-search />
</div>
```

You should now see the search component on the home page and the jobs page. 

Let's add an action to the form. Open the `/resources/views/components/search.blade.php` file and add the `action` attribute to the form tag. We are also using a method of GET.

```html
<form
  class="block mx-5 md:mx-auto md:space-x-2"
  method="GET"
  action="{{ route('jobs.search') }}"
></form>
```

The page will show an error because the route does not exist. Let's create the route. Open the `routes/web.php` file and add the following route.

```php
Route::get('/jobs/search', [JobController::class, 'search'])->name('jobs.search');
```

Add it above the job resource routes.

In the next lesson, we will add the controller method.
