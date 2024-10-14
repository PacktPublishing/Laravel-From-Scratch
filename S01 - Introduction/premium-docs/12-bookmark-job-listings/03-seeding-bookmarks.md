# Seeding Bookmarks

Before we move on, lets make it so that when we run our seeder, it adds random job listings as bookmarks for our test user.

## Return The Test user

First, we need to return the user from the `/database/seeders/TestUserSeeder.php` file:

```php
public function run(): any
{
    $user = User::create([
        'name' => 'Test User',
        'email' => 'test@test.com',
        'email_verified_at' => Carbon::now(),
        'password' => Hash::make('12345678'),
    ]);

    return $user;
}
```

## Bookmark Seeder

Let's now create a bookmark seeder. Run the following command to generate a new seeder:

```bash
php artisan make:seeder BookmarkSeeder
```

Open the `database/seeders/BookmarkSeeder.php` file and add the following imports:

```php
use App\Models\User;
use App\Models\Job;
```

Now add the following `run` method:

```php
 public function run(): void
{
    // Get the test user
    $testUser = User::where('email', 'test@test.com')->firstOrFail();

    // Get all job IDs
    $jobIds = Job::pluck('id')->toArray();

    // Randomly select job IDs to bookmark
    $randomJobIds = array_rand($jobIds, 3); // Change 3 to however many you want to bookmark

    // Attach the selected jobs as bookmarks for the test user
    foreach ($randomJobIds as $jobId) {
        $testUser->bookmarkedJobs()->attach($jobIds[$jobId]);
    }
}
```

## Update `DatabseSeeder.php`

Open the `database/seeders/DatabaseSeeder.php` file and truncate the new `job_user_bookmarks` table and run the `BookmarkSeeder` seeder:

```php
 public function run(): void
    {
        // Truncate tables
        DB::table('job_listings')->truncate();
        DB::table('users')->truncate();
        DB::table('job_user_bookmarks')->truncate();

        $this->call(TestUserSeeder::class);
        $this->call(RandomUserSeeder::class);
        $this->call(JobSeeder::class);
        $this->call(BookmarkSeeder::class);
    }
```

Now run the following command to seed the database:

```bash
php artisan db:seed
```

You should now see the test user has 3 random job listings bookmarked.
