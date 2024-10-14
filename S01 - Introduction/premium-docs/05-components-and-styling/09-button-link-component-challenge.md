# Button Link Component Challenge

In this challenge, I want you to create a new component called `ButtonLink` and use it for the `Create Job` link that is formatted as a button.

This component should get passed in the following props:

- url - URL the button link goes to
- icon - Optional icon
- bgClass - Class for the background. Default: 'bg-yellow-500'
- hoverClass - Class for the hover color. Default: 'hover:bg-yellow-600'
- textClass - Class for the text color. Default: 'text-black'

When you embed the button link component, it should look like this:

```php
<x-button-link url="/jobs/create" type="button" icon="edit">Create Job</x-button-link>
```

You should be able to pass in a class for the background, hover and text. If not, it uses the defaults that you describe in the `@props` directive.

<details>
  <summary>Click For Solution</summary>

Let's create a button component. Run the following command:

```bash
php artisan make:component ButtonLink
```

Let's add the props at the top of the `views/components/button-link.blade.php` file:

```php
@props([
'url' => '/',
'icon' => null,
'bgClass' => 'bg-yellow-500',
'hoverClass' => 'hover:bg-yellow-600',
'textClass' => 'text-black'
])
```

Just like the nav link, we have the url and icon. I also added the `bgClass`, `hoverClass`, and `textClass` props so we can change the background color, hover color, and text color of the button. Now add the following code to the `views/components/button-link.blade.php` file:

```php
<a href="{{ $url }}"
    class="{{$bgClass}} {{$hoverClass}} {{$textClass}} px-4 py-2 rounded hover:shadow-md transition duration-300">
    @if($icon)
    <i class="fa fa-{{ $icon }} mr-1"></i>
    @endif
    {{$slot}}
</a>
```

Now you can use the button link component to create a button link. Let's test it out.

In the `views/components/header.blade.php` file, replace the create job link with the following:

```html
<x-button-link url="/jobs/create" icon="edit">Create Job</x-button-link>
```

That's it for our nav links. We will get to the mobile nav links in the next lesson.
</details>
