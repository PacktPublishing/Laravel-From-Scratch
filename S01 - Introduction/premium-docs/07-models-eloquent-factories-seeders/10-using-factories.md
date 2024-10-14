# Using Factories

In this lesson, we will learn how to use factories. Factories are a way to define the attributes of a model in a reusable way. They allow you to define a blueprint for creating model instances with predefined attributes. This is useful when you need to seed your database with sample data or when you need to create model instances in your tests.

Laravel provides a factory class that you can use to define factories for your models. Factories are typically stored in the `database/factories` directory of your Laravel application.

If we look in the `database/factories` directory, we will see a file called `UserFactory.php`.

As you can see, in their most basic form, factories are classes that extend Laravel's base `Factory` class and define a `definition` method that returns the default set of attribute values that should be applied when creating a model using the factory.

Here is what the `definition` method looks like in the `UserFactory.php` file:

```php
public function definition(): array
{
    return [
        'name' => fake()->name(),
        'email' => fake()->unique()->safeEmail(),
        'email_verified_at' => now(),
        'password' => static::$password ??= Hash::make('password'),
        'remember_token' => Str::random(10),
    ];
}
```

Laravel comes bundles with a library called Faker that allows you to generate fake data. This is useful when you need to seed your database with sample data or when you need to create model instances in your tests.

In this case, it will generate the following:

- **name**: A random name
- **email**: A random email address that is unique
- **email_verified_at**: A timestamp of right now
- **password**: A hashed password of the string `password`
- **remember_token**: A random string of 10 characters

## Running Factories

We can create something called a seeder that will run factories, but we can also run them within our application, in tests as well as within Tinker. Let's use the user factory to create some users. Open up Tinker by running `php artisan tinker` and run the following command:

```php
\App\Models\User::factory()->create();
```

This will create a single user. Let's create 10 more by using the `count` method:

```php
\App\Models\User::factory()->count(10)->create();
```

Now you should have 11 users in your database. You can check with the following command:

```php
\App\Models\User::all();
```

As you can see these are verified users. There is a date for the field `email_verified_at`. However, if you wanted a user that was not verified, you can use the `unverified` method:

```php
\App\Models\User::factory()->unverified()->create();
```

This user will have a null value for the `email_verified_at` field.

Now that you know what a factory is and how to use it, let's create a factory for our `JobListing` model in the next lesson.
