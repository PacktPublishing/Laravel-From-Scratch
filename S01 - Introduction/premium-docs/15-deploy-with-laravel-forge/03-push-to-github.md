# Push To Github

We will bew using Laravel Forge and Digital Ocean to deploy our application. In order to get the files onto the server, we need to push our code to Github. Many of you probably already have done this, but if you haven't, here is how you do it.

## Disable Mailing

Since I did not go through the Mailtrap compliance yet, I'm going to disable the sending of emails when a user applys to a job. Open the `app/Http/controllers/ApplicantController.php` and comment out the following line:

```php
// Mail::to($job->user->email)->send(new JobApplied($application, $job));
```

After you do the compliance form, you can uncomment the line again.

I would also suggest adding the following line to your .gitignore file to prevent the theme_files from pushing to your repo:

```
/_theme_files
```

## Push To Github

If you have not created a Github account yet, you can do so here: https://github.com/

Initialize a git repository in your project folder if you have not done so already.

```bash
git init
```

Add the files to the repository.

```bash
git add .
```

Commit the files.

```bash
git commit -m "Initial commit"
```

Create a new repository on Github.

Go to the repository settings and copy the URL.

```bash
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPOSITORY.git
```

Push the files to Github.

```bash
git push -u origin main
```

Now your files should be on Github and we are ready to move to the next step.
