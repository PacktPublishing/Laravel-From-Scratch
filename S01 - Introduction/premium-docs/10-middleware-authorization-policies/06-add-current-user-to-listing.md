# Add Current User To Listing

We have full authentication implemented in our application. However, we still need to implement authorization. Right now, anyone can edit or delete any listing. We need to implement authorization so that only the user who created a listing can edit or delete it.

## Add User ID When Creating a Listing

The first step is to add a user ID to the listing when it is created. If you open the file `/app/Http/Controllers/JobController.php`, you will see that the `store` method has this line:

```php
// Add the hardcoded user_id
$validatedData['user_id'] = 1;
```

This line is hardcoded to the user ID of 1. We need to change this to the user ID of the currently authenticated user. We can do this by adding the following line to the `store` method:

```php
// Add the user ID of the current user
$validatedData['user_id'] = auth()->user()->id;
```

Now, log in and create a new job listing. If you check the database, you will see that the user ID of the listing is the user ID of the currently authenticated user.

## Add Authorization to the Edit and Delete Buttons

Right now, the edit and delete buttons on the listings are always visible. Let's make it so the user has to be logged in and the user who created the listing can see the edit and delete buttons. In the next couple videos we are going to simplify this a bit by creating something called a policy and using a directive called `@can`. But for now, we will just do a manual condition.

Open the file `/resources/views/jobs/show.blade.php` and change the edit and delete buttons to the following:

````html
@auth @if (auth()->user()->id === $job->user_id)
<div class="flex space-x-3 ml-4">
  <a
    href="{{ route('jobs.edit', $job->id) }}"
    class="px-4 py-2 bg-blue-500 hover:bg-blue-600 text-white rounded"
    >Edit</a
  >
  <!-- Delete Form -->
  <form
    method="POST"
    action="{{ route('jobs.destroy', $job->id) }}"
    onsubmit="return confirm('Are you sure you want to delete this job?');"
  >
    @csrf @method('DELETE')
    <button
      type="submit"
      class="px-4 py-2 bg-red-500 hover:bg-red-600 text-white rounded"
    >
      Delete
    </button>
  </form>
  <!-- End Delete Form -->
</div>
@endif @endauth ```
````

We are checking if the user is logged in and if the user ID of the currently authenticated user is the same as the user ID of the listing. If so, we show the edit and delete buttons.

This is fine but in the next lesson, I want to show you how to use the `@can` directive to do this by creating what we call a "policy".
