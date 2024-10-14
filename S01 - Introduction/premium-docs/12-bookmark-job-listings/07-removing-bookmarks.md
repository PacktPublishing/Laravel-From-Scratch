# Removing bookmarks

Now, we want to be able to remove the bookmarks. The heavy lifting is done. We already have the button submitting to the `destroys` route. We just need to add the functionality to remove the bookmark.


## Delete Bookmark Route

Open the routes file and add the delete route in the group:

```php
Route::middleware('auth')->group(function () {
  Route::get('/bookmarks', [BookmarkController::class, 'index'])->name('bookmarks.index');
  Route::post('/bookmarks/{job}', [BookmarkController::class, 'store'])->name('bookmarks.store');
  Route::delete('/bookmarks/{job}', [BookmarkController::class, 'destroy'])->name('bookmarks.destroy');
});
```

Open the `app/Http/Controllers/BookmarkController.php` file. Add the following code for the `destroy` method:

```php
// @desc   Remove a bookmark
// @route  DELETE /bookmarks/{job}
public function destroy(Job $job): RedirectResponse
{
    $user = Auth::user();

    // Check if the job is bookmarked before trying to remove it
    if (!$user->bookmarkedJobs()->where('job_id', $job->id)->exists()) {
        return back()->with('error', 'Job is not bookmarked.');
    }

    // Remove the bookmark
    $user->bookmarkedJobs()->detach($job->id);

    return back()->with('status', 'Job removed from bookmarks successfully.');
}

```

We check if the user is logged in. If they are not, we redirect them back to the previous page with a message. If they are logged in, we detach the bookmark from the user and redirect them back to the previous page with a message.

## Edit Button

We want to show a remove link/form if the user already has the job bookmarked. Add the following to the `resources/views/jobs.show.blade.php` file:

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
  action="{{ auth()->user()->bookmarkedJobs()->where('job_id', $job->id)->exists() ? route('bookmarks.destroy', $job->id) : route('bookmarks.store', $job->id) }}"
  method="POST"
  class="mt-10"
>
  @csrf 
  @if (auth()->user()->bookmarkedJobs()->where('job_id', $job->id)->exists()) 
    @method('DELETE')
    <button
      type="submit"
      class="bg-red-500 hover:bg-red-600 text-white font-bold w-full py-2 px-4 rounded-full flex items-center justify-center"
    >
      <i class="fas fa-bookmark mr-3"></i> Remove Bookmark
    </button>
  @else
    <button
      type="submit"
      class="bg-blue-500 hover:bg-blue-600 text-white font-bold w-full py-2 px-4 rounded-full flex items-center justify-center"
    >
      <i class="fas fa-bookmark mr-3"></i> Bookmark Listing
    </button>
  @endif
</form>
@endguest
```

We are checking if the bookmark exists and if it does, use the destroy route and change the text and styles
