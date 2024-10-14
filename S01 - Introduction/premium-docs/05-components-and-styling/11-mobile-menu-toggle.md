# Mobile Menu Toggle

This is going to be a very quick and simple lesson. We want to make the toggle work. Now ultimatley, when we need to add some interactive JavaScript, I woud suggest using Alpine.js, which is a lightweight JavaScript framework that provides reactivity and declarative rendering in your HTML markup. So you don't even have to write any JavaScript for things like toggling content and modals. We'll be using this later, but for now we'll just have a few lines of vanilla JavaScript.

Create a file at `/public/js/script.js` and add the following JavaScript:

```javascript
document.querySelector('#hamburger').addEventListener('click', function () {
  const menu = document.getElementById('mobile-menu');
  menu.classList.toggle('hidden');
});
```

This is for toggling the mobile menu.

## `asset` Helper Function

We can include these files in the layout with the `asset` helper function. This function generates a URL for an asset file.

Open the `/resources/views/components/layout.blade.php` file and add the following line to the bottom of the body section:


```html
<script src="{{ asset('js/script.js') }}"></script>
```

Your toggle button for the mobile menu should work now.
