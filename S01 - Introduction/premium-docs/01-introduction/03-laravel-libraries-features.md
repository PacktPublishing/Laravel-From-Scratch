# Laravel Libraries

Laravel is one of the most feature-packed web frameworks that exist. It has a ton of libraries and features built in. I talked a little bit about some of these in the last video, but this is an exhaustive list of what is included in the framework. We will be using just about all of these in the course.

### Built-in Laravel Components

1. **Blade Templating Engine**  
   Blade is Laravel's default templating engine for rendering views. We can pass data from the database or snywhere else into our views. There's also a component system now and we construct our UI like we would with a frontend framework like React. And of course Laravel is also great for APIs. So you can return JSON and use React or Vue or anything else for your frontend.

2. **Eloquent ORM**  
   Eloquent is Laravel's built-in ORM for interacting with databases. So we don't need to wrote raw SQL queries. It has a very elegany syntax for fetching, creating, updating, etc.

3. **Artisan CLI**  
   Command-line tool for managing Laravel applications. You can do everything from run database migrations to create controllers and models, run the dev server and so on.

4. **Tinker**  
    REPL (Read-Eval-Print Loop) for interacting with your application. You can do just about anything you can do from your code in a command line.

5. **Laravel's Routing**  
   The routing system is very dynamic and easy to use. Handing url patterns and ataching middleware grouping routes. You can generate resource routes.

6. **Validation**  
   Laravel has built in validation for form inputs.

7. **Session Management**  
   Built-in session handling.

8. **Cache**  
   Built-in caching system with support for various cache drivers.

9. **Authentication**  
   FOr authentication, you have all kinds of options. You can build it from scratch, which is what we'll be doing but you can also use scaffolding with something called Laravel Breeze. You basically run a command and it sets up the authentication along with the pages or views and forms to go with it. 

10. **Mailing**  
    Basic mail sending functionality using Laravel's `Mail` facade.

11. **Database Migrations**  
    Tools for managing and applying database schema changes.

12. **Logging**  
    Built-in logging functionality with support for various log channels.

13. **Testing**  
    PHPUnit testing framework integration for running unit and feature tests.

14. **Configuration Management**  
    Built-in configuration management using `.env` files.

15. **CSRF Protection**  
    Cross-Site Request Forgery protection built into forms and routes.

16. **Password Hashing**  
    Built-in password hashing functionality using Bcrypt.

17. **Laravel Collections**  
    Collection class for working with arrays and data more efficiently.

18. **Factories & Seeders**  
    Factories and seeders allow you to generate data for your models.

19. **Faker Library**  
    Faker is a library that allows you to generate very specific types of data like phone numbers, emails, job titles, etc.

20. **Carbon**  
    Library for working with dates and times.

As you can see, this is a massive list of features and tools that Laravel provides out of the box. You also have other tools that are avaialable like Sanctum for API authentication, Horizon for monitoring queues, Dusk for browser automation and many more that you can install or configure.

In the next section, we are going to get setup with PHP and Laravel.
