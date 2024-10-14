# Customizing The Pagination View

Right now we have a prev and next button, but what if we want to style it differently and add individual page numbers? Right now, that code is not available to us in our views. However we can publish the pagination view and customize it.

Open a terminal and run the following command:

```bash
artisan vendor:publish --tag=laravel-pagination
```

This will publish the pagination view into the `resources/views/vendor/pagination` directory. There will be multiple files in there and it depends on what CSS framework you are using. I am using Tailwind CSS, so I will edit the `tailwind.blade.php` file.

Open the `tailwind.blade.php` file and wipe away all the code and add the following:

```html
@if ($paginator->hasPages())
<nav
  role="navigation"
  aria-label="Pagination Navigation"
  class="flex justify-center"
>
  {{-- Previous Page Link --}} @if ($paginator->onFirstPage())
  <span class="px-4 py-2 bg-gray-300 text-gray-500 rounded-l-lg">Previous</span>
  @else
  <a
    href="{{ $paginator->previousPageUrl() }}"
    rel="prev"
    class="px-4 py-2 bg-blue-500 text-white rounded-l-lg hover:bg-blue-600"
    >Previous</a
  >
  @endif {{-- Pagination Elements --}} 
  @foreach ($elements as $element) 
    {{--"Three Dots" Separator --}} 
    @if (is_string($element))
        <span class="px-4 py-2 bg-gray-300 text-gray-500">{{ $element }}</span>
    @endif 
    {{-- Array Of Links --}} 
    @if (is_array($element)) 
      @foreach ($element as $page => $url) 
        @if ($page == $paginator->currentPage())
          <span class="px-4 py-2 bg-blue-500 text-white ">{{ $page }}</span>
        @else
          <a
            href="{{ $url }}"
            class="px-4 py-2 bg-gray-200 text-gray-700 hover:bg-blue-600 hover:text-white"
            >{{ $page }}</a
          >
        @endif 
      @endforeach 
    @endif 
  @endforeach 
  {{-- Next Page Link --}} 
  @if( $paginator->hasMorePages())
    <a
      href="{{ $paginator->nextPageUrl() }}"
      rel="next"
      class="px-4 py-2 bg-blue-500 text-white rounded-r-lg hover:bg-blue-600"
      >Next</a
    >
  @else
    <span class="px-4 py-2 bg-gray-300 text-gray-500 rounded-r-lg">Next</span>
  @endif
</nav>
@endif
```

We are using the same HTML and styles from our template. We are just making it dynamic by using loops, certain directives and variables.

You should now see the new pagination with the individual page numbers. You can customize it further by adding more classes or changing the styles.

Let's change the number of listings from 3 to 12 now that we are done with the pagination. Open the `app/Http/Controllers/JobController.php` file edit the line of code in the `index` method:

```php
 $jobs = Job::paginate(12);
```

Now if you have under 12 listings, you won't even see the pagination links.
