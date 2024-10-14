# Authentication Methods For Laravel

There are a ton of ways to implement authentication in Laravel. I just want to touch on some of the most common ones.

## Custom Authentication

Laravel makes it easy to build your own custom authentication system. You can use the `make:auth` command to scaffold the authentication views and routes. You can also use the `auth` middleware to protect routes. You can use the `Auth` facade to authenticate users. You can use the `Hash` facade to hash passwords. You can use the `bcrypt` helper function to hash.

## Laravel Breeze

Laravel Breeze is a minimalistic authentication starter kit that is included with Laravel. It is a great way to get started with authentication. It includes login, registration, password reset, email verification, and two-factor authentication. Laravel is a "batteries included" framework. It includes a ton of features that you can use right out of the box. Breeze is one of those features.

## Laravel Jetstream

Laravel Jetstream is a more feature-rich authentication starter kit that includes everything that Breeze has plus team management, API support, and more. Jetstream is built with Livewire and Inertia. Livewire is a full-stack framework for Laravel that makes building dynamic interfaces simple. Inertia is a library that allows you to build single-page applications using classic server-side routing and controllers. This is not something I would recommend for a small project for beginners. It is a great way to get started with Laravel if you are looking to build a larger application.

## Laravel Fortify

Laravel Fortify is a frontend agnostic authentication backend for Laravel. Fortify powers the registration, authentication, and two-factor authentication features of Laravel Jetstream.

## Laravel Sanctum

Laravel Sanctum is a lightweight package for API token authentication. Sanctum provides a simple way to authenticate single-page applications (SPAs) or mobile applications. Sanctum is great for building APIs that will be consumed by a frontend application built with React, Vue or another frontend framework.

## Soclialite

Laravel Socialite is an optional package that allows you to authenticate with OAuth providers like Facebook, Twitter, Google, and GitHub. Socialite is a great way to allow users to authenticate with your application using their existing social media accounts.

## What Are We Using?

I was a little confused on what to use for this project. Initially, I thought Breeze may be the way to go, however, as awesome as Breeze is for productivity, I don't think it's good for a course because you don't really understand what happen under the hood. It creates everything for you including routes, controllers, views, and models. So if you do use Breeze, you should use it at the very beginning of your project because it scaffolds everything for you.

Instead of using a starter kit like breeze, we'll build or own custom authentication with the helpers that Laravel gives us. This will reinforce our understanding of the framework and working with the MVC pattern.

With that said, I think it would still be a good idea to just show you how to get setup with Breeze. So we'll do that in the next lesson, which will be separate from our main project.
