# Show Job Applicants

Now we want to show the applicants to the job owner on their dashboard directly under the job listing.

## Update Dashboard Controller

First we need to make a small edit to the `DashboardController` `index` method to get the job applicants.

```php
// @desc   Show the dashboard
// @route  GET /dashboard
 public function show(Request $request): View
  {
      // Get the authenticated user
      $user = Auth::user();

      // Get all job listings for the authenticated user
      $jobs = Job::where('user_id', $user->id)->with('applicants')->get();

      return view('dashboard.show', compact('user', 'jobs'));
  }
```

We added `with('applicants')` to the `get()` method to get the applicants for each job.

## Show Applicants In View

Now in the `resources/views/dashboard/show.blade.php` file, we need to add the following code in the job listings just above the `@empty`:


```html
{{-- Applicants --}}
<div class="mt-4">
  <h4 class="text-lg font-semibold mb-2">Applicants</h4>
  @forelse($job->applicants as $applicant)
  <div class="py-2">
    <p class="text-gray-800">
      <strong>Name: </strong> {{$applicant->full_name}}
    </p>
    <p class="text-gray-800">
      <strong>Phone: </strong> {{$applicant->contact_phone}}
    </p>
    <p class="text-gray-800">
      <strong>Email: </strong> {{$applicant->contact_email}}
    </p>
    <p class="text-gray-800">
      <strong>Message: </strong> {{$applicant->message}}
    </p>
    <p class="text-gray-800 my-4">
      <a href="{{asset('storage/' . $applicant->resume_path)}}" class="text-blue-500 hover:underline" download>
        <i class="fas fa-download"></i> Downoad Resume
      </a>
    </p>
  </div>
```

It will show the fields as well as a download link for the resume.
