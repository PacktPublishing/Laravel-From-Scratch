# Text Editor Setup

As far as text editors and IDEs go, you have a lot of options. I recommend using [Visual Studio Code](https://code.visualstudio.com/). It is free, open source, and has a large community of developers that contribute to it and just has a ton of features and great extensions. It is also available on Mac, Windows and Linux, so you can use it on any operating system. This is what I will be using throughout the course.

Some other great options are [PHP Storm]](https://www.jetbrains.com/phpstorm/) and [Sublime Text](https://www.sublimetext.com/). These are not free, but Sublime Text does have a free trial.

So get one of those installed on your system.

## `code` Command

One of the first things that I would recommend doing is adding the `code` command to your PATH. This will allow you to open VS Code from the terminal by typing `code .` in the directory that you want to open. This is really handy and will save you a lot of time.

Open VS Code and press `CMD + SHIFT + P` on Mac or `CTRL + SHIFT + P` on Windows to open the command palette. Type "Shell Command: Install 'code' command in PATH" and press enter. This will add the `code` command to your PATH. Now you can open VS Code from the terminal by typing `code .`.

## VS Code Extensions

If you are using VS Code as I am, there are some handy extensions that I would suggest right off the bat. You can find these by clicking on the extensions icon on the left side of the editor.

- [PHP Intelephense](https://marketplace.visualstudio.com/items?itemName=bmewburn.vscode-intelephense-client) - This is a PHP code intelligence extension. It will help you with auto-completion, parameter hints, and more.
- [PHP Docblocker](https://marketplace.visualstudio.com/items?itemName=neilbrayfield.php-docblocker) - This will allow you to quickly add docblocks, which are multiple lined comments that describe what a function or a class does. I want to stick to writing clean code in this course and this will help us do that by documenting our code.
- [Laravel Snippets](https://marketplace.visualstudio.com/items?itemName=onecentlin.laravel5-snippets) - Provides snippets for Laravel 5 and above.
- [Laravel Blade Snippets](https://marketplace.visualstudio.com/items?itemName=onecentlin.laravel-blade) - Blade is a template engine used with Laravel and as far as I know, Laravel Snippets does not include snippets or highlighting for Blade files. So you definitely want this installed.

There are other extensions that you may like, but these 4 I definitely recommend.

## Formatting

As far as formatting goes, you can select "Format on Save" in your settings and it will automatically format your code when you save, which is really helpful. In order for it to work with PHP, I believe that you have to add the following to your main settings file so that it works with Intelephense.

Open your VSCode user settings JSON file by opening the command palette (CMD + SHIFT + P on Mac, CTRL + SHIFT + P on Windows) and typing "Open Settings (JSON)".

```json
"[php]": {
    "editor.formatOnSave": true,
    "editor.defaultFormatter": "bmewburn.vscode-intelephense-client"
},
```

#### Prettier

[Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode) is a great code formatter. Unfortunately it does not work with PHP out of the box, however, there is a plugin that you can install with NPM if you want.

In order to install the plugin, you need to have [Node.js](https://nodejs.org/en/) installed. You can download and install it from the website. Once you have it installed, you can open a terminal and run the following command from whichever directory you are working in:

```bash
npm init -y
npm i prettier @prettier/plugin-php
```

This is completely optional. I won't be using the Prettier plugin.
