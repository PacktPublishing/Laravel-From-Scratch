# Model Binding & Single Job Listing

We have the titles of the jobs on the /jobs page. Let's add links that will take them to the single listing page.

We already have a `show` method in the JobController. This is the method we will use to show a single listing. Right now, it is just returning a string. Let's create a view for it.

Create a file at `resources/views/jobs/show.blade.php` and add the following code:

```php
<x-layout>
  <h1 class='text-2xl'>{{ $job->title }}</h1>
  <p>{{ $job->description }}</p>
</x-layout>
```

Now, let's update the `show` method in the `JobController` to return this view:

```php
public function show(Job $job): View
{
    return view('jobs.show', compact('job'));
}
```

### Model Binding

We are using a feature called model binding. This is a feature of Laravel that allows us to type-hint a model in a controller method and Laravel will automatically fetch the model from the database based on the route parameter. In this case, the route parameter is `job`.

Then we are just loading the view and passing the job to it. You can pass as an array or use the compact helper function.

Now if you go to http://127.0.0.1:8000/jobs/1 you should see the job title and description.

Let's add the link to the title.

## `route` helper

The `route` helper is a function that allows us to generate a URL to a named route. In this case, we are using the `jobs.show` route.

Open the `resources/views/jobs/index.blade.php` file and add the following around the job title:

```php
<a href="{{ route('jobs.show', $job->id) }}">
  {{ $job->title }}
</a>
```

Now if you go to the /jobs page, you should see the job titles as links. Clicking on them will take you to the single job listing page.

Remember all of this will look much nicer and we will have a lot more fields. I just want to keep the data and views simple for now so you understand what's going on.
