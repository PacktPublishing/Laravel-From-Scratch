# Job User Bookmarks Migration

Now that we have total CRUD functionality for jobs and authentication with profiles, we are going to move on to bookmarking functionality where users can save or bookmark job listings that they are interested in.

This will require a new migration and table in the database, and a new controller, views. We also need to add new relationships. we will also add some seed data.

The table that we are creating with the migration is called a `pivot table` because it is a table that is used to join two other tables together. It is a table that is used to store the relationship between two other tables.

Earlier we created a `save` method in the `JobController`. You can delete that and delete the route that goes with it in the `routes/web.php` file. I mean you could use the Job controller for this stuff but I think it is more organized to have a separate controller for this.

## Add Relationships

We talked about relationships a while ago. We added a one to many relationship between jobs and users. Now we need a many to many relationship between jobs and users when it comes to bookmarks. A user can bookmark many jobs, and a job can be bookmarked by many users.

Open the `/app/Models/Job.php` file and add the following import:

```php
use Illuminate\Database\Eloquent\Relations\BelongsToMany;
```

Add the following method to the `Job` model:

```php
 public function bookmarkedByUsers(): BelongsToMany
{
    return $this->belongsToMany(User::class, 'job_user_bookmarks')->withTimestamps();
}
```

This will allow us to do things like `$job->bookmarkedByUsers` to get all the users that have bookmarked a job.

Open the `/app/Models/User.php` file and add the following import:

```php
use Illuminate\Database\Eloquent\Relations\BelongsToMany;
```

Add the following method to the `User` model:

```php
 public function bookmarkedJobs(): BelongsToMany
{
    return $this->belongsToMany(Job::class, 'job_user_bookmarks')->withTimestamps();
}
```

This will allow us to do things like `$user->bookmarkedJobs` to get all the jobs that a user has bookmarked.

We have the relationships set up, but we need to add the pivot table to the database.

## Create a New Migration

Let's start with the database migration. Run the following command to create a new migration:

```bash
php artisan make:migration create_job_user_bookmarks_table
```

Open the `/database/migrations/DATE_create_job_user_bookmarks_table.php` file and add the following code:

```php
<?php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

return new class extends Migration {
    public function up(): void
    {
        Schema::create('job_user_bookmarks', function (Blueprint $table) {
            $table->id();
            $table->foreignId('user_id')->constrained()->onDelete('cascade');
            $table->foreignId('job_id')->constrained('job_listings')->onDelete('cascade');
            $table->timestamps();
        });
    }

    public function down(): void
    {
        Schema::dropIfExists('job_user_bookmarks');
    }
};

```

We are creating a new table called `job_user_bookmarks` with two foreign keys, `user_id` and `job_id`. The `user_id` foreign key references the `id` column in the `users` table, and the `job_id` foreign key references the `id` column in the `jobs` table. We are also adding timestamps to the table.

Run the migration:

```bash
php artisan migrate
```

Check the database by using PG Admin, the command line or another tool and you should see the new table.
