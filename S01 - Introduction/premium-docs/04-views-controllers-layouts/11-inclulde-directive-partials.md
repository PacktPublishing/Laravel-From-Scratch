# `@include` Directive & Partial Views

In the previous chapter, we learned how to use the `@extends` directive to create a layout. In this chapter, we will learn how to use the `@include` directive to include a partial view in another view. There is a more modern way to use layouts using components, but we will cover that in a later chapter. I want you to understand both ways.

## Create A Partial View

Let's create a partial view that we can include in our views. Create a file at `resources/views/partials/navbar.blade.php` and add the following code:

```html
<nav>
  <a href="/">Home</a>
  <a href="/jobs">Jobs</a>
  <a href="/jobs/create">Create Job</a>
</nav>
```

## Use The Partial View

Now that we have a partial view, let's include it in our layout. Open the `layout.blade.php` file and replace the `<h1>` tag with the following code:

```html
@include('partials.navbar')
```

It should be right above the `<main>` tag. Now, the navbar will be included in every view that uses this layout.

Now you should see the menu on every page that uses this layout.

So you could proceed to build your website like this, but it is sort of the older way to do it. In the next section, we're really going to start on our project and we're going to use the more modern way of doing layouts using components.
