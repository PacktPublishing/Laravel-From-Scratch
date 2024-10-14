# Bookmarking Jobs

We can now see the jobs that we have created. Now we need to be able to bookmark them.

## Add Bookmark Route

Open the routes file and add the post route in the group:

```php
Route::middleware('auth')->group(function () {
  Route::get('/bookmarks', [BookmarkController::class, 'index'])->name('bookmarks.index');
  Route::post('/bookmarks/{job}', [BookmarkController::class, 'store'])->name('bookmarks.store');
});
```

## `store` Method

Let's add the `store` method to our `Job` controller. This method will allow us to bookmark a job.

```php
// @desc   Store a bookmark
// @route  POST /bookmarks/{job}
public function store(Job $job): RedirectResponse
{
    $user = Auth::user();

    // Check if the job is already bookmarked
    if ($user->bookmarkedJobs()->where('job_id', $job->id)->exists()) {
        return back()->with('status', 'Job is already bookmarked.');
    }

    // Create a new bookmark
    $user->bookmarkedJobs()->attach($job->id);

    return back()->with('status', 'Job bookmarked successfully.');
}
```

We are first checking if the job is already bookmarked. If it is, we are returning a message saying so. If it is not, we are creating a new bookmark.

## Bookmark Button

Let's open the `resources/views/jobs/show.blade.php` file. Right now there is just a link for the add bookmark button. We need to change it to a form. Replace it with the follwing:

```html
<!-- Bookmark Button -->
@guest
<p
  class="mt-10 bg-gray-200 text-gray-700 font-bold w-full py-2 px-4 rounded-full text-center"
>
  <i class="fas fa-info-circle mr-3"></i> You must be logged in to bookmark this
  job.
</p>
@else
<form
  action="{{ route('bookmarks.store', $job->id) }}"method="POST" class="mt-10">
  @csrf 
    <button
      type="submit"
      class="bg-blue-500 hover:bg-blue-600 text-white font-bold w-full py-2 px-4 rounded-full flex items-center justify-center"
    >
      <i class="fas fa-bookmark mr-3"></i> Bookmark Listing
    </button>
</form>
@endguest
```

If the user is not logged in, we are showing a message saying so. If the user is logged in, we are showing a form/button.

We should now be able to bookmark jobs and see them on the saved page. In the next lesson we will add the functionality to remove bookmarks.
