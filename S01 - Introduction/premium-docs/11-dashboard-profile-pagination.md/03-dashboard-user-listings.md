# Dashboard User Job Listings

Now we want the user's listings to be displayed on their dashboard page. We already have everything in place. In the controller, we are passing the jobs into the view.

Add the following to the dashboard view:

```html
<div class="bg-white p-8 rounded-lg shadow-md w-full">
  <h3 class="text-3xl text-center font-bold mb-4">My Job Listings</h3>
  @forelse ($jobs as $job)
  <div
    class="flex justify-between items-center border-b-2 border-gray-200 py-2"
  >
    <div>
      <h3 class="text-xl font-semibold">{{ $job->title }}</h3>
      <p class="text-gray-700">{{ $job->job_type }}</p>
    </div>
   <div class="flex space-x-4">
      <a
        href="{{ route('jobs.edit', $job->id) }}"
        class="bg-blue-500 hover:bg-blue-600 text-white px-4 py-2 rounded text-sm"
        >Edit</a
      >
      <form
        method="POST"
        action="{{ route('jobs.destroy', $job->id) }}"
        onsubmit="return confirm('Are you sure you want to delete this job?');"
      >
        @csrf @method('DELETE')
        <button
          type="submit"
          class="bg-red-500 hover:bg-red-600 text-white px-4 py-2 rounded text-sm"
        >
          Delete
        </button>
      </form>
    </div>
  </div>
  @empty
  <p class="text-gray-700">You have no job listings.</p>
  @endforelse
</div>
```

## Control Delete Redirect

Right now the jobs are showing fine and you can edit and delete them using the buttons. However right now when you delete a job from the dashboard page, you are redirected to the homepage. I don't want that. I want to stay on the dashboard page if we delete from this page.

First, we need to add a query string to the delete form action. Open the `resources/views/dashboard/index.blade.php` file and add the following to the delete form:

```php
<form method="POST" action="{{ route('jobs.destroy', $job->id) }}?from=dashboard" onsubmit="return confirm('Are you sure you want to delete this job?');">
```

We added `?from=dashboard` to the end of the route. This will add a query string to the URL when the form is submitted.

Open the `app/Http/Controllers/JobController.php` file and edit the `destroy` method by adding this line right above the redirect that is already there:

```php
 // Check if the request came from the dashboard page
if (request()->query('from') === 'dashboard') {
    return redirect()->route('dashboard.index')->with('success', 'Job listing deleted successfully!');
}
```

Now when you delete a job from the dashboard page, you will stay on that page.

You can run `php artisan db:seed` to get the listings back if you deleted them.
