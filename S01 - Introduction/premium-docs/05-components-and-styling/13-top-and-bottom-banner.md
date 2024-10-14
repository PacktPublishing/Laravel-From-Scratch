# Top & Bottom Banner Components

We have a couple other components to create. We have the top banner on the homepage which goes right under the hero section. We also have the bottom banner, which will go on the homepage as well as some other pages.

Let's start with the top banner. Run the following command to create a new component:

```bash
php artisan make:component TopBanner
```

Let's add the following code to the `/resources/views/components/top-banner.blade.php` file:

```html
<section class="bg-blue-900 text-white py-6 text-center">
  <div class="container mx-auto">
    <h2 class="text-3xl font-semibold">Unlock Your Career Potential</h2>
    <p class="text-lg mt-2">Discover the perfect job opportunity for you.</p>
  </div>
</section>
```

Now, add it to the `/resources/views/components/layout.blade.php` file and limit to the homepage just like the hero component:

```php
  @if(request()->is('/'))
    <x-hero />
    <x-top-banner />
  @endif
```

Let's make the a couple props for the heading and subheading. Update the `TopBanner` component like so:

```php
@props(['heading' => 'Unlock Your Career Potential', 'subheading' => 'Discover the perfect job opportunity for you'])

<section class="bg-blue-900 text-white py-6 text-center">
    <div class="container mx-auto">
        <h2 class="text-3xl font-semibold">
            {{ $heading }}
        </h2>
        <p class="text-lg mt-2">
            {{ $subheading }}
        </p>
    </div>
</section>
```

Now if you wanted to, you can pass in the heading and subheading.

## Bottom Banner Component

Now let's create the bottom banner component. Run the following command to create a new component:

```bash
php artisan make:component BottomBanner
```

Add the following code to the `/resources/views/components/bottom-banner.blade.php` file:

```html
<section class="container mx-auto my-6">
  <div
    class="bg-blue-800 text-white rounded p-4 flex items-center justify-between"
  >
    <div>
      <h2 class="text-xl font-semibold">Looking to hire?</h2>
      <p class="text-gray-200 text-lg mt-2">
        Post your job listing now and find the perfect candidate.
      </p>
    </div>
    <a
      href="create-job.html"
      class="bg-yellow-500 hover:bg-yellow-600 text-black px-4 py-2 rounded hover:shadow-md transition duration-300"
    >
      <i class="fa fa-edit"></i> Create Job
    </a>
  </div>
</section>
```

We can also add a heading and subheading component here. Another thing that we can do, since it uses the same button as the header is we can use the `ButtonLink` component that we created earlier. Update the `BottomBanner` component like so:

```php
@props(['heading' => 'Looking to hire?', 'subheading' => 'Post your job listing now and find the perfect
candidate'])

<section class="container mx-auto my-6">
    <div class="bg-blue-800 text-white rounded p-4 flex items-center justify-between">
        <div>
            <h2 class="text-xl font-semibold">{{$heading}}</h2>
            <p class="text-gray-200 text-lg mt-2">
                {{$subheading}}
            </p>
        </div>
        <x-button-link url="/jobs/create" type="button" icon="edit">Create Job</x-button-link>
    </div>
</section>
```

Since the bottom banner does not need to span the whole page width, we can put it right in the home view. Update the `resources/views/pages/home.blade.php` file like so:

```php
<x-layout>
    <x-bottom-banner />
</x-layout>
```

Now it should show on the homepage. We will add it to the other pages later.
