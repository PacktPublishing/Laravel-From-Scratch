# Hero Component

Now let's work on the hero component. This will have a background image and a search form. The search form will be put into it's own component much later, so we won't worry about that just yet. I just want to get it displayed on the homepage.

Run the following command to generate a new component called `Hero`.

```bash
php artisan make:component Hero
```

Open the newly created `/resources/views/components/hero.blade.php` file and replace the content with the following:

```html
<section
  class="hero relative bg-cover bg-center bg-no-repeat h-72 flex items-center"
>
  <div class="overlay"></div>
  <div class="container mx-auto text-center z-10">
    <h2 class="text-5xl text-white font-bold mb-8">Find Your Dream Job</h2>
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
  </div>
</section>
```

Like I said, the form will be it's own component. We will handle that later.

## Background Image

To show the background image, we need some custom CSS and we need to bring the image into the folder structure. Copy the file `_theme_files/images/hero.jpg` to `/public/images/hero.jpg`.

Create a file at `/public/css/style.css` and add the following CSS:

```css
.overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.8); /* Adjust opacity as needed */
  z-index: 1;
}

.hero {
  background-image: url('../images/hero.jpg');
}
```

Open the `/resources/views/components/layout.blade.php` file and add the following line to the head section:

```html
<link rel="stylesheet" href="{{ asset('css/style.css') }}" />
```

## Title Prop

Let's make the H2 text a prop that can be passed in. Add the following to the top of the file:

```php
@props(['title' => 'Find Your Dream Job'])
```

Then replace the H2 text with the following:

```html
<h2 class="text-4xl text-white font-bold mb-4">{{ $title }}</h2>
```

## Limiting the Hero To The Homepage

We have an issue here. I only want the hero component on the homepage but remember all pages are wrapped in a `<main class="container mx-auto p-4 mt-4">` tag. This means that any component in the homepage will be restricted to the container. The hero needs to go all the way across the page. The solution is to put this component in the layout but limit it to the homepage by using the `request` helper function.

Open the `/resources/views/components/layout.blade.php` file and add the following code above the opening `main` tag:

```php
  @if(request()->is('/'))
  <x-hero />
  @endif
```

This will only show the hero component on the homepage.





