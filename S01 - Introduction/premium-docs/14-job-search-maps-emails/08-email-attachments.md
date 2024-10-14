# Email Attachments

In this lesson, we will send the resume as an email attachment.

We are already passing the entire `$application` variable to the email, which includes the `resume_path` property. We can use this property to attach the resume to the email.

Open the `app/Mail/JobApplied.php` file and import the following:

```php
use Illuminate\Mail\Mailables\Attachment;
```

Add the following to the `attachements` method:

```php
public function attachments(): array
{
    // Attach the resume if it exists
    $attachments = [];
    if ($this->application->resume_path) {
        $attachments[] = Attachment::fromPath(storage_path('app/public/' . $this->application->resume_path))
            ->as($this->application->resume_path)
            ->withMime('application/pdf');
    }

    return $attachments;
}
```

We are using the `Attachment::fromPath` method to attach the resume. We are using the `storage_path` helper to get the path to the resume. We are using the `withMime` method to specify the MIME type of the attachment.

Now submit an application with a resume and it will be sent as an attachment.
