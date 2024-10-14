# Test User Seeder

We already have the ability to wipe the database jobs and users and recreate 10 new ones with the following command:

```bash
php artisan db:seed
```

I also want it to create a test user so that I don't have to keep registering a new user every time I want to test something.

Let's create a new seeder:

```bash
php artisan make:seeder TestUserSeeder
```

Open the file `database/seeders/TestUserSeeder.php` and add the following code:

```php
<?php

namespace Database\Seeders;

use Illuminate\Database\Seeder;
use Illuminate\Support\Facades\Hash;
use App\Models\User;
use Carbon\Carbon;

class TestUserSeeder extends Seeder
{
    /**
     * Run the database seeds.
     */
    public function run(): void
    {
        User::create([
            'name' => 'Test User',
            'email' => 'test@test.com',
            'email_verified_at' => Carbon::now(),
            'password' => Hash::make('12345678'),
        ]);
    }
}
```

Now we need to add the seeder to the `DatabaseSeeder` class. Open the file `database/seeders/DatabaseSeeder.php` and add the line to call the new seeder:

```php
public function run(): void
{
    // Truncate tables
    DB::table('job_listings')->truncate();
    DB::table('users')->truncate();

    $this->call(TestUserSeeder::class); // Add this line
    $this->call(RandomUserSeeder::class);
    $this->call(JobSeeder::class);
}
```

## Assign the User ID To Listings

Let's make it so that a couple of the listings are created by the test user. Open the file `database/seeders/JobSeeder.php` and change the `run` method to the following:

```php
 public function run(): void
{
    // Load job listings data
    $jobListings = include database_path('seeders/data/job_listings.php');

    // Get the ID of the user created by TestUserSeeder
    $testUserId = User::where('email', 'test@test.com')->value('id');

    // Get all other user IDs
    $userIds = User::where('email', '!=', 'test@test.com')->pluck('id')->toArray();

    foreach ($jobListings as $index => &$listing) {
        if ($index < 2) {
            // Assign the first two job listings to the test user
            $listing['user_id'] = $testUserId;
        } else {
            // Assign the rest to random users
            $listing['user_id'] = $userIds[array_rand($userIds)];
        }
        // Add timestamps
        $listing['created_at'] = now();
        $listing['updated_at'] = now();
    }

    // Insert job listings
    DB::table('job_listings')->insert($jobListings);
}
```

We get the test user ID and all other user IDs. Then we loop through the job listings and assign the first two to the test user and the rest to random users.

Now every time we run `php artisan db:seed`, it will create a new user with the email `test@test.com` and the password `12345678`. It will also create 10 new job listings, with the first two being created by the test user and the rest being created by random users.
