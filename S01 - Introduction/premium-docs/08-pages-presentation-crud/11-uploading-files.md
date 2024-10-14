# Uploading Files

We are able to create a new job listing, but we are missing the company logo upload functionality. Let's do that now.

We already have the table column for the image path in our database and we also have the image upload field in the form. We just need to add the logic to handle the file upload.

Let's open the `JobController` and add this right above where we create the job:

```php
dd($request->file('company_logo'));
```

This will print out the file object and stop the script. Now, go to the job creation form and create a new job listing. You should see the file object printed out.
This includes things like the file name, the file extension, the file mime type, file path, etc.

There is a method called `store()` that we can use on this object. This method will store the file in the `storage/app/public` directory. We can also specify a directory within that public directory.

#### Create a Symlink

Before we can access the file from the browser, we need to create a symlink. Run the following command:

```bash
php artisan storage:link
```

This will create a symlink from the `public/storage` directory to the `storage/app/public` directory.

Now remove the `dd` and add this to the `store()` method:

```php
 // Check if a file was uploaded
if ($request->hasFile('company_logo')) {
    // Store the file and get the path
    $path = $request->file('company_logo')->store('logos', 'public');

    // Add the path to the validated data array
    $validatedData['company_logo'] = $path;
}
```

Now try and upload a listing with a file.

You will not see the image in the website yet, but you should see the image in the `storage/app/public/logos` directory.

The URL to the image would be:

```
http://127.0.0.1:8000/storage/logos/YOURIMAGE.png
```

## Update the Card Component & Details Page Image Path

Now that we have the image path, we need to update the card component and the job details page to display the image.

Open the `/resources/views/components/job-card.blade.php` file and change the image path to the following:

```html
<img
  src="/storage/{{ $job->company_logo }}"
  alt="{{$job->company_name}}"
  class="w-14"
/>
```

Now open the `/resources/views/job-details.blade.php` file and change the image path to the following:

```html
<img
  src="/storage/{{$job->company_logo}}"
  alt="{{$job->company_name}}"
  class="w-full rounded-lg mb-4 m-auto"
/>
```

Now you will not see any of the other images. However, if you want to keep the sample images, just move them to the `storage/app/public/logos` directory. Now you will see your sample data images and your newly uploaded images.
