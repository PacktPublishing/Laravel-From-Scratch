# Header Component & `url()` Helper

We are going to add the content and styling to the header component and also look at the `url()` helper.

We already have our Header component at `resources/views/components/header.blade.php`. Let's update this file.

This will be the first time that we copy some HTML from the theme files. I put my theme files, right in the root of the project. You can put them anywhere you want. We want to open `_theme_files/index.html` and copy the `<header>` section and everything inside it. It should look like this:

```html
<header class="bg-blue-900 text-white p-4">
  <div class="container mx-auto flex justify-between items-center">
    <h1 class="text-3xl font-semibold">
      <a href="index.html">Workopia</a>
    </h1>
    <nav class="hidden md:flex items-center space-x-4">
      <a href="jobs.html" class="text-white hover:underline py-2">All Jobs</a>
      <a href="saved-jobs.html" class="text-white hover:underline py-2"
        >Saved Jobs</a
      >
      <a href="login.html" class="text-white hover:underline py-2">Login</a>
      <a href="register.html" class="text-white hover:underline py-2"
        >Register</a
      >
      <a href="dashboard.html" class="text-white hover:underline py-2">
        <i class="fa fa-gauge mr-1"></i> Dashboard
      </a>
      <a
        href="create-job.html"
        class="bg-yellow-500 hover:bg-yellow-600 text-black px-4 py-2 rounded hover:shadow-md transition duration-300"
      >
        <i class="fa fa-edit"></i> Create Job
      </a>
    </nav>
    <button id="hamburger" class="text-white md:hidden flex items-center">
      <i class="fa fa-bars text-2xl"></i>
    </button>
  </div>
  <!-- Mobile Menu -->
  <div
    id="mobile-menu"
    class="hidden md:hidden bg-blue-900 text-white mt-5 pb-4 space-y-2"
  >
    <a href="jobs.html" class="block px-4 py-2 hover:bg-blue-700">All Jobs</a>
    <a href="saved-jobs.html" class="block px-4 py-2 hover:bg-blue-700"
      >Saved Jobs</a
    >
    <a href="dashboard.html" class="block px-4 py-2 hover:bg-blue-700"
      >Dashboard</a
    >
    <a href="login.html" class="block px-4 py-2 hover:bg-blue-700">Login</a>
    <a href="register.html" class="block px-4 py-2 hover:bg-blue-700"
      >Register</a
    >
    <a
      href="create-job.html"
      class="block px-4 py-2 bg-yellow-500 hover:bg-yellow-600 text-black"
    >
      <i class="fa fa-edit"></i> Create Job
    </a>
  </div>
</header>
```

Paste it within the `/resources/views/components/header.blade.php` file.

Right, now it has all of the links. Some of them will only show when logged in or logged out, but we will get to that later. Right now, I just want to focus on the header being displayed and styled.

If you go to the homepage now, you should see the Header at the top of the page. It is missing the icons and the mobile dropdown menu does not work because it needs a little JavaScript. We will get to that in a bit.

## url() Helper

We have a few links in the Header. We need to update them to use the `url()` helper. This is a Laravel helper that generates a URL for the given path. This is useful because it will generate the correct URL for the current environment. For example, if you are in a local environment, it will generate `http://localhost:8000/jobs`. If you are in a production environment, it will generate `https://workopia.com/jobs`.

Update the links in the Header to use the `url()` helper. Here is an example:

Change this:

```html
<a href="jobs.html" class="text-white hover:underline py-2">All Jobs</a>
```

To this:

```html
<a href="{{ url('/jobs') }}" class="text-white hover:underline py-2"
  >All Jobs</a
>
```

Use the slash before the route name. Otherwise, you could get urls like `http://localhost:8000/jobs/jobs`.

Do this for all the links in the Header. Here are the links:

- All Jobs - `url('/jobs')`
- Saved Jobs - `url('/jobs/saved')`
- Dashboard - `url('/dashboard')`
- Create Job - `url('/jobs/create')`
- Login - `url('/login')`
- Register - `url('/register')`

Now you can navigate to the different pages using the Header links. Most of them will not work obviously because we have not created the routes yet. There is also a `route()` helper for named routes. We will use that for most other links but for the navigation links, we will use the `url()` helper.

The code should now look like this:

```html
<header class="bg-blue-900 text-white p-4">
  <div class="container mx-auto flex justify-between items-center">
    <h1 class="text-3xl font-semibold">
      <a href="{{ url('/') }}">Workopia</a>
    </h1>
    <nav class="hidden md:flex items-center space-x-4">
      <a href="{{ url('/jobs') }}" class="text-white hover:underline py-2"
        >All Jobs</a
      >
      <a href="{{ url('/jobs/saved') }}" class="text-white hover:underline py-2"
        >Saved Jobs</a
      >
      <a href="{{ url('/login') }}" class="text-white hover:underline py-2"
        >Login</a
      >
      <a href="{{ url('/register') }}" class="text-white hover:underline py-2"
        >Register</a
      >
      <a href="{{ url('/dashboard') }}" class="text-white hover:underline py-2">
        <i class="fa fa-gauge mr-1"></i> Dashboard
      </a>
      <a
        href="{{ url('/jobs/create') }}"
        class="bg-yellow-500 hover:bg-yellow-600 text-black px-4 py-2 rounded hover:shadow-md transition duration-300"
      >
        <i class="fa fa-edit"></i> Create Job
      </a>
    </nav>
    <button id="hamburger" class="text-white md:hidden flex items-center">
      <i class="fa fa-bars text-2xl"></i>
    </button>
  </div>
  <!-- Mobile Menu -->
  <div
    id="mobile-menu"
    class="hidden md:hidden bg-blue-900 text-white mt-5 pb-4 space-y-2"
  >
    <a href="{{ url('/jobs') }}" class="block px-4 py-2 hover:bg-blue-700"
      >All Jobs</a
    >
    <a href="{{ url('/jobs/saved') }}" class="block px-4 py-2 hover:bg-blue-700"
      >Saved Jobs</a
    >
    <a href="{{ url('/dashboard') }}" class="block px-4 py-2 hover:bg-blue-700"
      >Dashboard</a
    >
    <a href="{{ url('/login') }}" class="block px-4 py-2 hover:bg-blue-700"
      >Login</a
    >
    <a href="{{ url('/register') }}" class="block px-4 py-2 hover:bg-blue-700"
      >Register</a
    >
    <a
      href="{{ url('/jobs/create') }}"
      class="block px-4 py-2 bg-yellow-500 hover:bg-yellow-600 text-black"
    >
      <i class="fa fa-edit"></i> Create Job
    </a>
  </div>
</header>
```

Now your links should show on larger screens. We will get to the mobile links soon.

## Adding Font Awesome

Let's open the `views/components/layout.blade.php` file and add the following code to the `<head>` tag:

```html
<link
  rel="stylesheet"
  href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.6.0/css/all.min.css"
  integrity="sha512-Kc323vGBEqzTmouAECnVceyQqyqdsSiqLQISBL29aUW4U/M7pSPA/gEUZQqv1cwx4OnYxTxve5UMg5GT6L4JJg=="
  crossorigin="anonymous"
  referrerpolicy="no-referrer"
/>
```

Now the icons should show.
