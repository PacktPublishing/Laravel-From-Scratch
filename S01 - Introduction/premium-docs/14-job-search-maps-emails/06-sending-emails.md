# Sending Emails

We can send emails from Laravel. What I would like to do is notify the user when someone applies to their job. We can do this by sending an email. We're going to be using Mailtrap for this, which is a an emailing platform for testing and sending emails in production. We're going to use it for both. There's a very generous free teir that let's us send up to 200 emails per day. Obviously if you're building a production site then you'll want to look into the premium plans, but the free plan is more than enough for this project.

Since we're building locally, we can't just simply send emails from Laravel. Mailtrap gives us a sandbox smtp server to use in development. So we're going to get that setup now.

## Set Up Mailtrap

Let's start by setting up Mailtrap. Go to [Mailtrap](https://mailtrap.io/) and sign up for an account. Once you are signed up, click on "Start Testing" under "Email Testing". This will allow us to test emails in our local environment.

Once you do that, click on the "Add Inbox" button and give it a name. I will call mine "Workopia". You will then see your inbox. Click on that and where it says "Code Samples", click on PHP and choose "Laravel 9+" from the dropdown. This will give you the configuration that you need to add to your `.env` file. It will look something like this:

```bash
MAIL_MAILER=smtp
MAIL_HOST=sandbox.smtp.mailtrap.io
MAIL_PORT=2525
MAIL_USERNAME=kj5k3j54k3j45
MAIL_PASSWORD=********er495
```

Up above click on the password and you will see an option to "Copy Password". Paste all of this in your `.env` file replacing the existing `MAIL_` variables.

I am also going to change the MAIL_FROM_ADDRESS to `noreply@workopia.dev`. I actually have the domain `workopia.dev`. I would suggest using a domain that you own.

## Mailables

In Laravel, we can send emails using a Mailable. A Mailable is a class that contains the logic for sending an email. We can create a Mailable by running the following command:

```bash
php artisan make:mail JobApplied
```

Now open the `app/Mail/JobApplied.php` file. There are some methods such as `envelope`, `content` and `attachments`.

Within the `content` method, we can add the view that we want to use. Let's add the following:

```php
public function content(): Content
{
  return new Content(
      view: 'emails.job-applied',
  );
}
```

For the subject, we can add the following:

```php
public function envelope(): Envelope
{
    return new Envelope(
        subject: 'New Job Application',
    );
}
```

## Create View

Let's create a view for our email. Create a file at `resources/views/emails/job-applied.blade.php`. In this file, we can add the HTML that we want to send in the email. For now, just add the following:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Workopia Job Application</title>
  </head>

  <body>
    <p>There has been a new job application to your Workopia listing</p>

    <p>Login to your Workopia account to view the application.</p>
  </body>
</html>
```

## Send Email

Now that we have our Mailable set up, we can send the email. Let's send the email when someone applies to a job. Open the `ApplicantController` and

Add the following imports:

```php
use App\Mail\JobApplied;
use Illuminate\Support\Facades\Mail;
```

Add the following code to the `store` method just above the redirect:

```php
// Send email to owner
 Mail::to($job->user->email)->send(new JobApplied());
```

Now try and apply for a job. Open your Mailtrap inbox and you should see the email that we just sent. It will have the job owner's email address as the recipient.

You may want to send data in the email. We will do that in the next lesson.
