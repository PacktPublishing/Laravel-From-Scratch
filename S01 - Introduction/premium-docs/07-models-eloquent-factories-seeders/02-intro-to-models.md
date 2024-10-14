# Intro To Models

So we know all about routes, controllers, and views. We also learned how to integrate a database and use migrations, but what about models? What are they and how do they fit into the MVC pattern?

Models are the M in MVC. They are responsible for interacting with the database. They represent the data in your application and are used to perform database operations like creating, reading, updating, and deleting records. In Laravel, models are typically stored in the `app/Models` directory.

## Eloqent ORM

Laravel uses Eloquent ORM (Object-Relational Mapping) to interact with the database. Eloquent is an implementation of the Active Record pattern. It allows you to work with database records as objects. This makes it easy to query the database and perform CRUD operations. This allows us to keep our models clean and simple. There are tons of pre-built methods that we can use to interact with the database.

## Create A Basic Model

Before we get into Eloqent ORM, let's create a basic model. We can use Artisan to create models, but we will create this one manually. Create a new file called `Job.php` in the `app/Models` directory. Add the following code:

```php
<?php
namespace App\Models;

class Job
{
  static public function all(): array
  {
    return [
      [
        "id" => 1,
        "title" => "Software Engineer",
        "description" => "Design and develop high-quality software applications, collaborating with teams and ensuring efficient solutions.",
      ],
      [
        "id" => 2,
        "title" => "Marketing Specialist",
        "description" => "Develop and execute marketing campaigns, conduct market research, and drive brand engagement.",
      ],
      [
        "id" => 3,
        "title" => "Customer Support Representative",
        "description" => "Provide excellent customer service, troubleshoot customer issues, and maintain customer satisfaction.",
      ],
    ];
  }
}
```

The namespace `App\Models` tells Laravel where to find the model. There could be other classes with the same name of `Job` in different namespaces. Namespaces help us categorize our classes and avoid conflicts.

We are creating a static class. This class has a static method called `all` that returns an array of job listings. It is also typed to an array type, which is optional.

This is a simple example to demonstrate how models work. Usually the data would come from a database, but we are just hardcoding it for now.

## Use The Model

Now that we have a model, let's use it in our controller. Open the `JobController.php` file and import the `Job` model at the top:

```php
use App\Models\Job;
```

Now replace the `index` method with the following code:

```php
 public function index(): View
{
    $title = 'Available Jobs';
    $jobs = Job::all();
    return view('jobs/index', compact('title', 'jobs'));
}
```

We are now passing the jobs to the view. We can access the jobs in the view using the `$jobs` variable. You'll get an error now because before we were passing an array of strings, but now we are passing an associative array. We need to update the view to handle this new data structure.

Open the `jobs/index.blade.php` file and replace the `foreach` loop with the following code:

```php
@foreach($jobs as $job)
  <li>{{$job['title']}}</li>
@endforeach
```

Now we are looping through the jobs and displaying the title. You can also display the description with `$job['description']`, but we are not keeping this code. In fact you can delete the `app/models/Job.php` file because we will generate a new one in the next video.

In the next lesson, we will learn how to use Eloquent ORM to interact with the database.
