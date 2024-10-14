# Get & Show Bookmarks

We have our table in the database, now let's add the controller and routes to get the bookmarks and the view to show them.


## Bookmark Route

Open the `routes/web.php` file and add the following route grouped with the auth middleware:

```php
Route::middleware('auth')->group(function () {
  Route::get('/bookmarks', [BookmarkController::class, 'index'])->name('bookmarks.index');
});

```

be sure to import the `BookmarkController` class:

```php
use App\Http\Controllers\BookmarkController;
```

## Bookmark Controller

Open a terminal and type the following command to generate a new controller:

```bash
php artisan make:controller BookmarkController
```

Now open the `app/Http/Controllers/BookmarkController.php` file and add the following imports:

```php
use App\Models\Job;
use Illuminate\Http\RedirectResponse;
use Illuminate\View\View;
use Illuminate\Support\Facades\Auth;
```

Now add the following `index` method:

```php
public function index(): View
{
  $user = Auth::user();

  $bookmarks = $user->bookmarkedbookmarks()->paginate(10);
  dd($jobs);
```

The `bookmarkedJobs` pertains to the method we created in the `User` model. The `paginate(10)` method will paginate the results.

Let's test this by going to the `bookmarks` route in the browser. You should see a dump of the object with the collection of bookmarks.

Let's return a view instead:

```php
// @desc   Show all bookmarks for user
// @route  GET bookmarks
public function index(): View
{
    $user = Auth::user();

    $bookmarks = $user->bookmarkedJobs()->paginate(10);

    return view('jobs.bookmarked')->with('bookmarks', $bookmarks);
}
```



## Show Bookmarks in View

Create a file at `/resources/views/jobs/bookmarked.blade.php` and add the following:

```php
<x-layout>
  <h2 class="text-center text-3xl mb-4 font-bold border border-gray-300 p-3">
    Bookmarked Jobs
  </h2>
  <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-6">
    @forelse ($bookmarks as $bookmark)
    <x-job-card :job="$bookmark" />
    @empty
    <p class="text-center text-gray-500">No bookmarks available</p>
    @endforelse
  </div>

  {{ $bookmarks->links() }}
</x-layout>
```

You should now see the cards for the jobs that you bookmarked.

