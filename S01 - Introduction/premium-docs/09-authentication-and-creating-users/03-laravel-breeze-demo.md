# Laravel Breeze Demo

As I explained in the last lesson, we're going to build our own authentication system. However, I still want to show you how to scaffold a project with Breeze. This will give you a good idea of what Breeze does for you. It's a great way to get started with authentication.

## What Is Included With Breeze?

Breeze includes routes, controllers, models and views with styled working forms for:

- Login
- Registration
- Password Reset
- Email Verification
- Two-Factor Authentication

## New Laravel Project

DO NOT do any of this in our current Workpoia project. Open your terminal in a completely new folder. Run the following command to create a new Laravel project:

```bash
composer create-project laravel/laravel breeze-demo
cd breeze-demo
```

## Install Breeze

Run the following command to install Breeze:

```bash
composer require laravel/breeze --dev
```

Now we can run the following command to setup the controllers, routes, views and other resources:

```bash
php artisan breeze:install
```

You will then be asked which Breeze stack do you want to use. These are the options:

- Blade with Alpine
- Livewire (Volt Class API) with Alpine
- Livewire (Volt Functional API) with Alpine
- React with Inertia
- Vue with Inertia
- API only

This shows you how many different types of applications that you can build with Laravel. We're going to use the default option and type in `blade` and hit enter.

I will say no for dark mode.

Just hit enter when it asks about tests.

## Run The Server

Now you can run the following command to start the server. I will use a different port since I am still running the Workpoia project on port 8000.:

```bash
php artisan serve --port 8001
```

Now you can visit `http://localhost:8001` and you should see a login and register link. You can click on the register link and create a new user. You will then be redirected to the dashboard. There is also a profile page that you can visit.

How insane is that? You have a fully functioning authentication system that you created in literally seconds. This is the power of Laravel.

I am going to stop the server and delete the project. I just wanted to show you the awesomeness. If you want to inspect the code and see the routes, controllers, etc, you can do that.

I am going to get back to our project and create a custom authentication system.
