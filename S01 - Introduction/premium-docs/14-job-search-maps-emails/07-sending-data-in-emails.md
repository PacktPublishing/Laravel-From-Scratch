# Sending Data In Emails

We have the email being sent to the job owner. Let's add some data to the email. I want the job title and all the application data. We can do this by passing data to the Mailable class.

Open the `app/Http/controllers/ApplicantController.php` file and pass in the `$application` and `$job` variables to the Mailable class.

```php
Mail::to($job->user->email)->send(new JobApplied($application, $job));
```

## Update The Mailable Class

Open the `app/Mail/JobApplied.php` file and

Add the `$application` variable to the class.

```php
class JobApplied extends Mailable {
use Queueable, SerializesModels;

public $application; // Add this line
public $job; // Add this line

    //..
```

Update the constructor to accept the `$application` variable.

```php
public function __construct($application, $job)
{
    $this->application = $application;
    $this->job = $job;
}
```

## Update The View

Change the view to the following:

```php
<!DOCTYPE html>
<html>

<head>
  <title>Workopia Job Application</title>
</head>

<body>
  <p>There has been a new job application to your Workopia listing</p>

  <p><strong>Job Title:</strong> {{ $job->title }}</p>

  <p><strong>Application Details:</strong></p>

  <p><strong>Full Name:</strong> {{ $application->full_name }}</p>
  <p><strong>Contact Number:</strong> {{ $application->contact_number }}</p>
  <p><strong>Contact Email:</strong> {{ $application->contact_email }}</p>
  <p><strong>Message:</strong> {{ $application->message }}</p>
  <p><strong>Location:</strong> {{ $application->location }}</p>

   <p>Log in to your Workopia account to view the application</p>
</body>

</html>
```

In the next lesson, we will send the resume pdf as an email attachment.
