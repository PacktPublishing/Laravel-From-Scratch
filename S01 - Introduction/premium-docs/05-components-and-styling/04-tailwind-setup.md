# Tailwind CSS & Vite Hot Reloading

Now we are going to set up Tailwind CSS in our Laravel project. Tailwind CSS is a utility-first CSS framework that is easy to use and customize. It is a great choice for building modern and responsive web applications.

There are a few ways to implement Tailwind. We can use the CDN, but that's not really reccomended for production. We're going to install Tailwind Using NPM. This way, we can customize the configuration and build the CSS file. So the CSS will only include the classes that we are using, which will make the file size smaller. Also, we're going to be using Vite as our frontend dev tool which includes hot reloading. Up to this point, if you're using Laravel Herd or something other than the Artisan server, we've had to referesh manually after every change. After setting up Vite and running the server, it should refresh right when we save a file, which is nice.

## Tailwind Setup Using NPM

If you go to https://tailwindcss.com/docs/guides/laravel there are instructions on how to set up Tailwind in a Laravel project. We will follow along with these instructions.

NPM stands for Node Package Manager. It is a package manager for JavaScript. It is used to install and manage packages for a project. If you are coming from the JavaScript world, you are probably already familiar with NPM. If not, don't worry, it is easy to use.

You do need to install Node.js to use NPM. You can download it from https://nodejs.org/en/. Once you have Node.js installed, you will have NPM installed as well.

## Install Tailwind CSS

First, open a terminal window up in the project directory. Run the following command to install Tailwind CSS:

```bash
npm install -D tailwindcss postcss autoprefixer
```

Now, generate the Tailwind configuration file by running the following command:

```bash
npx tailwindcss init -p
```

Open the `tailwind.config.js` file and add the following code:

```javascript
/** @type {import('tailwindcss').Config} */
export default {
  content: [
    './resources/**/*.blade.php',
    './resources/**/*.js',
    './resources/**/*.vue',
  ],
  theme: {
    extend: {},
  },
  plugins: [],
};
```

This will tell Tailwind to look for classes in the Blade files, JavaScript files, and Vue files. I know we are not using Vue at this point, but it is good to have it set up in case we decide to use it later. Vue and Laravel are often used together.

Now add the following code to the `resources/css/app.css` file:

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

This will import the Tailwind CSS styles into our project.

Now we just need to include the CSS file in the layout. Open the `resources/views/components/layout.blade.php` file and add the following code just above the title:

```html
@vite('resources/css/app.css')
```

## Build Tailwind CSS

Now we need to build the Tailwind CSS file. We can have it watch for changes by running the following command:

```bash
npm run dev
```

So from now on, you will run `npm run dev` to build the Tailwind CSS file. This will watch for changes and rebuild the file when changes are made. You also have hot reloading available.
