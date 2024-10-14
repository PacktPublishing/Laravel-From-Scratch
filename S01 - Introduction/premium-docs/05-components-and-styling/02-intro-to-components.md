# Intro To Components

Components were introduced in Laravel 7.0. Components provide a way to encapsulate HTML, CSS, and JavaScript into reusable pieces that can be used throughout your application. They support both class-based components (using PHP classes) and anonymous components (using simple Blade templates). This helps in keeping your views organized and maintainable. If you are coming from a frontend JavaScript framework like React or Vue, you will feel right at home with Laravel components.

In this chapter, we will learn how to create and use components in Laravel.

## Create A Component

Let's create a component that we can use in our views. Run the following command to create a new component:

```bash
php artisan make:component Header
```

This command will create a new component class at `app/View/Components/Header.php` as well as a Blade template at `resources/views/components/header.blade.php`. For the most part, you will work in the template because this is where you will put the HTML for the component. But let's take a look at the component class first.

- It has a namespace and some imports that are needed for the class to function properly.

- The class extends `Component`, which is a base class that provides some useful methods and properties for the component.

- The \_\_construct method is where you can pass data into your component. If your component needs any initialization or data when it’s created, you can do that here. For example, you could add parameters to the constructor and assign them to class properties.

- The render() is a method that returns the view associated with this component. This method tells Laravel which Blade view file to use when rendering the component.

For most components, we won't need to do much here, but I want you to know what it does.

Open the view at `resources/views/components/header.blade.php`. This is where you will put the HTML for the component.

Add the following code for now:

```html
<nav>
  <a href="/">Home</a>
  <a href="/jobs">Jobs</a>
  <a href="/jobs/create">Create Job</a>
</nav>
```

## Use The Component

Now that we have a component, let's use it in our layout. Open the `layout.blade.php` file and replace the `<h1>` tag with the following code:

```html
<x-header />
```

We use the `x-` prefix to tell Laravel that we want to use a component. The `x-` prefix is a convention that is used to indicate that the tag is a component.

Now you can delete the `partials/header.blade.php` file because we are using the component instead. You can delete the entire `partials` directory.

## Sub-Folders

You can also create sub-folders inside the `components` directory. For example, let's create a folder called `inputs` and create a file called `text.blade.php`. This is something that we will be doing later, so we can create the folder and file now.

In the `text.blade.php` file, add the following code:

```html
<input type="text" />
```

Now, let's use this component in our layout just to see how we use it. Open the `layout.blade.php` file and replace the `<input>` tag with the following code:

```html
<x-inputs.text />
```

So we add the `x-` prefix then the name of the folder and the file name. This is how you reference components in sub-folders.

You can delete this line now. But keep the folder and file because we will be using it later.

In the next lesson, I will show you how to use components for your layout.
