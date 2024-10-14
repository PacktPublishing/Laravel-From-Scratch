# Homepage Jobs

We want to show the latest 6 job listings on the homepage. This means we need to go into the `app/Http/Controllers/HomeController.php` file and make some changes.

Right now, the `index` method just returns a view. We want to return the view with the latest 6 job listings. We can do this by using the `Job` model. We can get the latest 6 job listings by using the `latest` method and then limiting the results to 6.

Bring in the `Job` model by adding the following line to the top of the file:

```php
use App\Models\Job;
```

Here is the updated `index` method:

```php
public function index(): View
{
    $jobs = Job::latest()->limit(6)->get();

    return view('pages.home')->with('jobs', $jobs);
}
```

## Update the Home View

Now open the `resources/views/pages/home.blade.php` file and add the wrapper div and loop over the jobs and output the job card component. We will also add the "Recent Jobs" heading and a link to the `/jobs` page. Here is the updated code:

```html
<x-layout>
  <h2 class="text-center text-3xl mb-4 font-bold border border-gray-300 p-3">
    Recent Jobs
  </h2>
  <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-6">
    @forelse($jobs as $job)
    <x-job-card :job="$job" />
    @empty
    <p>No jobs found</p>
    @endforelse
  </div>
  <a href="{{ route('jobs.index') }}" class="block text-xl text-center">
    <i class="fa fa-arrow-alt-circle-right"></i> Show All Jobs
  </a>
  <x-bottom-banner />
</x-layout>
```

Alright, our homepage looks great. Let's move on to the job details page.
