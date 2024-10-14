# Simple Job Pagination

Right now, all jobs will be displayed at once even if there are hundreds of them. This is not a good idea. We should paginate them. Laravel has a built-in pagination system. We will use that to paginate the jobs.

## Job Controller

The first step is to edit the `index` method in the `JobController` to paginate the jobs. Change the following code:

```php
$jobs = Job::all();
```

To this:

```php
$jobs = Job::paginate(3);
```

I am only using `3` to test it out. I will change it to a higher number later.

If you go to the `/jobs` route, you will only see three listings. If you manually type in `/jobs?page=2`, you will see the next three listings.

## Add Links

Now let's add the links. Open the `resources/views/jobs/index.blade.php` file and add the following code right above the closing `</x-layout>`:

```html
<!-- Pagination Links -->
<div class="mt-4">{{ $jobs->links() }}</div>
```

It's as simple as that to add pagination in Laravel.

One issue though is that you are bound to the style of the pagination links. We also only have prev and next and not the individual page numbers. We can change this by publishing the pagination view and customizing it. I will show you how to do that in the next lesson.
