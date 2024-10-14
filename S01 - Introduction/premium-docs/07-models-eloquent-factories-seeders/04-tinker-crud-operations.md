# Tinker & CRUD Operations

In the last lesson, we created a model and used it to fetch data from the database. In this lesson, I want to show you how to create, read update and delete data using Eloquent. We will be using Tinker, which is a command line tool, however, when we want to do this stuff in our application, we use the same code.

Let's run Tinker:

```bash
php artisan tinker
```

## Access Models & Data

We can access the Job model by using the fully qualified namespace:

```php
>>> App\Models\Job::all()
```

This will get our listings, which right now we do not have any.

We can see the schema of the model by using the `getColumnListing` method on the `Schema` facade:

```php
Schema::getColumnListing('job_listings');
```

One thing I want to do is create a variable for the model namespace. This will make it easier to type and will help us avoid errors.

```php
>>> $job = App\Models\Job::class
```

Now you should be able to do the following:

```php
>>> $job::all()
```

And see the same result.

## Adding Data

Let's add some data to the database. We can do this by creating a new instance of the model and setting the properties:

```php
$Job::create([
    'title' => 'Job One',
    'description' => 'This is an description for job one',
]);
```

You should see a result like this:

```php
App\Models\Job {#5996
    title: "Job One",
    description: "This is an description for job one",
    updated_at: "2024-08-13 11:43:25",
    created_at: "2024-08-13 11:43:25",
    id: 1,
  }
```

Let's add few more:

```php
$job::create([
  'title' => 'Job Two',
  'description' => 'This is an description for job two',
]);
```

```php
$job::create([
  'title' => 'Job Three',
  'description' => 'This is an description for job three',
]);
```

```php
$job::create([
  'title' => 'Job Four',
  'description' => 'This is an description for job four',
]);
```

Now list the jobs:

```php
>>> $job::all()
```

You should see all jobs listed.

## Finding Data

We can use the `find` method to find a specific job. We just need to pass in the ID.

Let's find the first job:

```php
>>> $job::find(1)
```

You should see the first job.

## Updating Data

Let's update the first job:

```php
>>> $job::find(1)->update(['title' => 'Updated Job One'])
```

Now check it:

```php
>>> $job::find(1)
```

You should see the updated job.

## Deleting Data

Let's delete the second job:

```php
>>> $job::find(2)->delete()
```

Now check the jobs:

```php
>>> $job::all()
```

You should see the second job is gone.

So it's as easy as that to perform CRUD operations with Tinker. If you go to the jobs page, you should see the jobs listed there as well.
