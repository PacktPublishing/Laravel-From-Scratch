# Create a New Job

So we know how to fetch jobs within our application. We also know how to create them from within Tinker. But how do we actually create them from within our application? It actually isn't much different than what we did in Tinker. We already have a form on the create page if you have been following along. It is extremely ugly at the moment but that's okay. Remember, I am not interested in making things look good yet or having all of the data for the job listings. We are only dealing with the title and description at the moment for simplicity.

The form is being loaded from the Job Controller's create method, which loads the view at `resources/views/jobs/create.blade.php`.

The form is being submitted to the store method on the Job Controller, which right now looks like this:

```php
 public function store(Request $request): string
{
    $title = $request->input('title');
    $description = $request->input('description');

    return "Title: $title, Description: $description";
}
```

So we already know how to get the data using the Request object. We also know how to create a new job using the Eloquent ORM from what we did with Tinker. Let's apply that knowledge to our application.

First, let's update the store method to create a new job:

```php
public function store(Request $request): RedirectResponse
{
    $title = $request->input('title');
    $description = $request->input('description');

    Job::create([
        'title' => $title,
        'description' => $description
    ]);

    return redirect()->route('jobs.index');
}
```

Since we are using the `RedirectResponse` class, we need to import it at the top of the file:

```php
use Illuminate\Http\RedirectResponse;
```

Now when we submit the form, it will create a new job and redirect us to the jobs index page. We can see the job that we just created.

Now that we are able to fetch and create jobs, I think the next step is to add the rest of the fields to the database table and then work on the styling of the application.
