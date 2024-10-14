# Prevent Multiple Applications

I don't want the same user to be able to submit an application to the same job listing. Let's open the `app/Http/controllers/ApplicantController.php` file and change the `store` method to the following:

```php
public function store(Request $request, Job $job): RedirectResponse
{
    // Check if the user has already applied for the job
    $existingApplication = Applicant::where('job_id', $job->id)
                                    ->where('user_id', auth()->id())
                                    ->exists();

    if ($existingApplication) {
        return redirect()->back()->with('status', 'You have already applied to this job.');
    }

    // Validate incoming data
    $validatedData = $request->validate([
        'full_name' => 'required|string',
        'contact_phone' => 'string',
        'contact_email' => 'required|string|email',
        'message' => 'string',
        'location' => 'string',
        'resume' => 'required|file|mimes:pdf|max:2048',
    ]);

    // Handle resume upload
    if ($request->hasFile('resume')) {
        $path = $request->file('resume')->store('resumes', 'public');
        $validatedData['resume_path'] = $path;
    }

    // Store the application
    $application = new Applicant($validatedData);
    $application->job_id = $job->id;
    $application->user_id = auth()->id();
    $application->save();

    return redirect()->back()->with('success', 'Your application has been submitted.');
}

```

Now a user should only be able to apply once.