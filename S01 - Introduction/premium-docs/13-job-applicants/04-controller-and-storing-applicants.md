# Applicant Controller & Storing Applicants

Now that we have the form to submit the job application, we need to create the controller and routes to handle the form submission and store the data and upload the resume.

## Applicant Routes

Let's create the routes for the applicant controller. We need a route to the `store` method, which will handle the form submission.

Open the `web.php` file and add the following import:

``php
use App\Http\Controllers\ApplicantController;
````

Now add the route:

```php
Route::post('/jobs/{job}/apply', [ApplicantController::class, 'store'])->name('applicants.store');
````

Put it above the job resource routes.

## Applicant Controller

Next, let's create the `ApplicantController` and the `store` method to handle the form submission. Open the terminal and run the following command:

```bash
php artisan make:controller ApplicantController
```

This will create the `ApplicantController` in the `app/Http/Controllers` directory. Open the `ApplicantController.php` file and add the following code:

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use App\Models\Job;
use App\Models\Applicant;
use Illuminate\Http\RedirectResponse;

class ApplicantController extends Controller
{
    // @desc   Store a new job application
    // @route  POST /jobs/{job}/apply
    public function store(Request $request, Job $job): RedirectResponse
    {
        // Validate the incoming request data
        $validatedData = $request->validate([
            'full_name' => 'required|string|max:255',
            'contact_number' => 'string|max:20',
            'contact_email' => 'required|email',
            'message' => 'string',
            'location' => 'string|max:255',
            'resume' => 'required|file|mimes:pdf|max:2048',
        ]);

        dd($validatedData);
    }
}
```

Be sure to import the `Job` and `Applicant` models at the top of the file.

## Form Submission

I have included a dummy resume.pdf in the files for this section but you can use any pdf. Make sure you have a pdf file ready to submit with the form.

Now submit your applicant form and you should see the data dumped to the screen.

The url should be something like `http://127.0.0.1:8000/jobs/5/apply`

## Storing The Resume

Replace the `dd` with the following code:

```php
 // Handle the resume file upload
if ($request->hasFile('resume')) {
    $path = $request->file('resume')->store('resumes', 'public');
    $validatedData['resume_path'] = $path;
}
```

We are checking if the resume file is present in the request. If it is, we are storing the file in the `public/resumes` directory and updating the `resume_path` field in the `validatedData` array.

## Saving The Applicant

Now let's save the applicant to the database:

```php

// Store the application
$application = new Application($validatedData);
$application->job_id = $job->id;
$application->user_id = auth()->id();
$application->save();

return redirect()->back()->with('success', 'Your application has been submitted!');
```

Here is the full `AppliantController.php` file:

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use App\Models\Job;
use App\Models\Applicant;
use Illuminate\Http\RedirectResponse;

class ApplicantController extends Controller
{
    public function store(Request $request, Job $job): RedirectResponse
    {
        // Validate the incoming request data
        $validatedData = $request->validate([
            'full_name' => 'required|string|max:255',
            'contact_number' => 'string|max:20',
            'contact_email' => 'required|email',
            'message' => 'string',
            'location' => 'string|max:255',
            'resume' => 'required|file|mimes:pdf|max:2048',
        ]);

        // Handle the resume file upload
        if ($request->hasFile('resume')) {
            $path = $request->file('resume')->store('resumes', 'public');
            $validatedData['resume_path'] = $path;
        }

        // Store the application
        $application = new Applicant($validatedData);
        $application->job_id = $job->id;
        $application->user_id = auth()->id();
        $application->save();

        return redirect()->back()->with('success', 'Your application has been submitted!');
    }
}
```

You should now be able to submit your application and see the data in the database.

# Clear Applicants On Seed

You could make it so some applicants are created when you run the seeder, but for now, let's clear the applicants table when we seed the database.

Open thee `DatabaseSeeder.php` file and add the following line under the other truncates:

```php
DB::table('applicants')->truncate();
```

Now when you run the seeder, the applicants table will be cleared.

```bash
php artisan db:seed
```

