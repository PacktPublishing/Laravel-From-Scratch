# Mobile Menu Link 

So we have the regular menu all set. Let's take care of the links in the mobile menu. These links classes differ a bit, so we can't just use the NavLink component as is. What I want to do is pass in a prop of `:mobile="true"` if it is a mobile link and it will then apply the correct classes.

Before we do anything though, we need to be able to see the mobile menu. We can not yet because we have not added the frontend JavaScript to toggle the mobile menu. We will do that in the next lesson. For now, let's remove the `hidden` class from the mobile menu in the header.

Remove the `hidden` and `md:hidden` class from the following code in the `header.blade.php` file:

```html
<nav
  div
  id="mobile-menu"
  class="hidden md:hidden bg-blue-900 text-white mt-5 pb-4 space-y-2"
></nav>
```

Open the `components/nav-link.blade.php` file and add an extra prop for "mobile":

```php
@props(['url' => '/', 'active' => false, 'icon' => null, 'mobile' => false])
```
Now add an if directive and add the mobile link classes:

```php
@if($mobile)
<a href="{{$url}}" class="block px-4 py-2 hover:bg-blue-700 {{$active ? 'text-yellow-500 font-bold' : ''}}">
    @if($icon)
    <i class="fa fa-{{$icon}}" mr-1"></i>
    @endif
    {{$slot}}
</a>
@else
<a href="{{$url}}" class="text-white hover:underline py-2 {{$active ? 'text-yellow-500 font-bold' : ''}}">
    @if($icon)
    <i class="fa fa-{{$icon}}" mr-1"></i>
    @endif
    {{$slot}}
</a>
@endif
```

Now replace the mobile menu links in the header with the following:

```html
<x-nav-link url="/jobs" :active="request()->is('jobs')" :mobile="true">All Jobs</x-nav-link>
<x-nav-link url="/jobs/saved" :active="request()->is('jobs/saved')" :mobile="true">Saved Jobs</x-nav-link>
<x-nav-link url="/login" :active="request()->is('login')" :mobile="true">Login</x-nav-link>
<x-nav-link url="/register" :active="request()->is('register')" :mobile="true">Register</x-nav-link>
<x-nav-link url="/dashboard" :active="request()->is('dashboard')" :mobile="true">Dashbaord</x-nav-link>
```

## Mobile Button Link

The only difference between the mobile button link and the ButtonLink component is that the mobile version has a class of `block`. So let's add a prop of `block` in the `components/button-link.blade.php` file:

```php
@props([
'url' => '/',
'icon' => null,
'bgClass' => 'bg-yellow-500',
'hoverClass' => 'hover:bg-yellow-600',
'textClass' => 'text-black',
'block' => false
])
```

Now add a ternary checking for that prop and if it is true, show a class of `block`:

```php

<a href="{{$url}}"
    class="{{$bgClass}} {{$hoverClass}} {{$textClass}} px-4 py-2 rounded hover:shadow-md transition duration-300 {{$block ? 'block' : ''}}">
    @if($icon)
    <i class="fa fa-{{$icon}}"></i>
    @endif
    {{$slot}}
</a>
```

Now the mobile menu should look the same. It is just using components for the links and button.

Now add the `hidden` and `md:hidden` class back to the mobile menu in the `header.blade.php` file:

```html
<nav
  id="mobile-menu"
  class="hidden md:hidden bg-blue-900 text-white mt-5 pb-4 space-y-2"
></nav>
```

In the next lesson, we will add the JavaScript to toggle the mobile menu as well as the image and css assets. We will also create the hero component.
