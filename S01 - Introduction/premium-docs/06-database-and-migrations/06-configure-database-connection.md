# Configure Database Connection

We now have PostgreSQL installed and we have a brand new database and user called workopia. We are going to configure our Laravel application to use this database.

Open the `.env` file in the root of your Laravel project. This file contains environment variables that are used to configure your application. You will see a bunch of variables that are used to configure your application. We are interested in the database configuration.

```env
DB_CONNECTION=pgsql
DB_HOST=127.0.0.1
DB_PORT=5432
DB_DATABASE=workopia
DB_USERNAME=workopia
DB_PASSWORD=password
```

These variables are used in the `config/database.php` file to configure the database connection.

## Test the Database Connection

Laravel comes bundled with a CLI tool called `tinker` that allows you to interact with your application from the command line. You can use this tool to test the database connection.

Run the following command to open the tinker shell:

```bash
php artisan tinker
```

This will open a new terminal window where you can interact with your application. We are going to tinker around with Tinker more later on, but right now, I just want to test the connection. We have access to a `DB` facade that allows you to interact with the database. It has a method called `select` that allows you to run SQL queries.

Run the following command to test the database connection:

```php
DB::select('SELECT version()')
```

This will return the version of PostgreSQL that is installed on your computer. If you see a version number, then you have successfully configured your database connection. If you are using SQLite or MySQL, you will see that information.

If you see an error, then there is an issue with your database connection. Check the `.env` file to make sure the database configuration is correct.

Run the following command to exit the tinker shell:

```php
exit
```
