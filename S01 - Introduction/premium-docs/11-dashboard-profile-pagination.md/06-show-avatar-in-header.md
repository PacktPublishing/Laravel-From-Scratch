# Show Avatar in Header

We are going to show the user's avatar in the header. I also want to show a default avatar if the user does not have one.

There is an image in the downloads for this lesson called `default-avatar.png`. You can use this image as the default avatar. You can use any image you want just rename it to `default-avatar.png`. Put this image in the `/storage/app/public/avatars/` directory.

## Update The Header Component

Open the `resources/views/components/header.blade.php` file and add this right under the "Create job" link. It will be right before the `@else` which is from the if statement that checks if the user is logged in.

```html
<!-- User Avatar -->
<div class="flex items-center space-x-3">
  @if(Auth::user()->avatar)
  <img
    src="{{ asset('storage/' . Auth::user()->avatar) }}"
    alt="{{ Auth::user()->name }}"
    class="w-10 h-10 rounded-full"
  />
  @else
  <img
    src="{{ asset('storage/avatars/default-avatar.png') }}"
    alt="{{ Auth::user()->name }}"
    class="w-10 h-10 rounded-full"
  />
  @endif
</div>
```

Now the user's avatar will show in the navbar. If the user does not have an avatar, the default avatar will show.

## Rearrange The Navbar

This is 100% up to you but I am going to rearrange the navbar a bit. I am going to get rid of the dashboard link and make the avatar the link to the dashboard. I am also going to move the logout link to the end.

Here is the final version of the `resources/views/components/header.blade.php` file.

```html
<header class="bg-blue-900 text-white p-4" x-data="{ open: false }">
  <div class="container mx-auto flex justify-between items-center">
    <h1 class="text-3xl font-semibold">
      <a href="{{ route('home') }}">Workopia</a>
    </h1>
    <nav class="hidden md:flex items-center space-x-4">
      <x-nav-link url="/" :active="request()->is('/')">Home</x-nav-link>
      <x-nav-link url="/jobs" :active="request()->is('jobs')"
        >All Jobs</x-nav-link
      >
      @auth
      <x-nav-link url="/jobs/saved" :active="request()->is('jobs/saved')"
        >Saved Jobs</x-nav-link
      >

      <x-button-link url="/jobs/create" type="button" icon="edit"
        >Create Job</x-button-link
      >

      <!-- User Avatar -->
      <div class="flex items-center space-x-3">
        <a href="{{ route('dashboard.show') }}">
          @if(Auth::user()->avatar)
          <img
            src="{{ asset('storage/' . Auth::user()->avatar) }}"
            alt="{{ Auth::user()->name }}"
            class="w-10 h-10 rounded-full"
          />
          @else
          <img
            src="{{ asset('storage/avatars/default-avatar.png') }}"
            alt="{{ Auth::user()->name }}"
            class="w-10 h-10 rounded-full"
          />
          @endif
        </a>
      </div>
      <form method="POST" action="{{ route('logout') }}">
        @csrf
        <button type="submit" class="text-white">
          <i class="fa fa-sign-out"></i> Logout
        </button>
      </form>
      @else
      <x-nav-link url="/login" :active="request()->is('login')"
        >Login</x-nav-link
      >
      <x-nav-link url="/register" :active="request()->is('register')"
        >Register</x-nav-link
      >
      @endauth
    </nav>
    <button
      @click="open = !open"
      class="text-white md:hidden flex items-center"
    >
      <i class="fa fa-bars text-2xl"></i>
    </button>
  </div>
  <!-- Mobile Menu -->
  <nav
    x-show="open"
    @click.away="open = false"
    class="md:hidden bg-blue-900 text-white mt-5 pb-4 space-y-2"
  >
    <x-mobile-nav-link url="/" :active="request()->is('/')"
      >Home</x-mobile-nav-link
    >
    <x-mobile-nav-link url="/jobs" :active="request()->is('jobs')"
      >All Jobs</x-mobile-nav-link
    >
    @auth
    <x-mobile-nav-link url="/jobs/saved" :active="request()->is('jobs/saved')"
      >Saved Jobs</x-mobile-nav-link
    >
    <x-mobile-nav-link
      url="/dashboard"
      :active="request()->is('dashboard')"
      icon="gauge"
      >Dashboard
    </x-mobile-nav-link>
    <form method="POST" action="{{ route('logout') }}">
      @csrf
      <button type="submit" class="text-white">
        <i class="fa fa-sign-out"></i> Logout
      </button>
    </form>
    <div class="py-2">
      <x-button-link url="/jobs/create" type="button" icon="edit"
        >Create Job</x-button-link
      >
    </div>
    @else
    <x-mobile-nav-link url="/login" :active="request()->is('login')"
      >Login</x-mobile-nav-link
    >
    <x-mobile-nav-link url="/register" :active="request()->is('register')"
      >Register</x-mobile-nav-link
    >
    @endauth
  </nav>
</header>
```
