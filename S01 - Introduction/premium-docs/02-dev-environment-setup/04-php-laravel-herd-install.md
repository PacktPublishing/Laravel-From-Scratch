# PHP & Laravel Herd Setup 

Now we're ready to get our dev environment setup. As I mentioned in the last video, there are a lot of different ways to install PHP and get Laravel up and running. If you already have a dev environment and PHP 8.3 is installed, you're fine. If not, I would suggest using Laravel Herd. Even if you don't want to use the Herd features, it's still the easiest way to get PHP installed and configured. 

Go to https://herd.laravel.com and download the installer. Go through the steps. The install and UI is a bit different depending on if you're on MacOS or Windows, but you get the same features.

Once you get through the install, open the control panel and you should see the NGINX server running. You should see options for your PHP version and a button that says "Open Sites". This is where all of your Laravel sites go. 

Let's create our Laravel website. If you aren't using Herd and you're still watching this video, I will show you how to install Laravel using Composer in a later video. It's up to you on how you want to setup your environment. This is definitely the easiest.

Click on "Add Site".

Select "New Laravel Project".

Select "No Starter Kit".

For the project name, add "Workopia".

Leave the default selection for path and tests and initialize a Git repo. It's up to you on how you want to handle version control, but if you want to deploy this project you will need to use Git.

Your project has been created and you have easy access to the terminal, Tinker, which is a command line tool. The project path and the URL.


You can also use the `php` command from anywhere on your machine. Open a terminal and type the following:

```bash
php --version
```

You should see the version number. For me it is 8.3.11.

You can also run the integrated PHP server if you want. Create a new folder called "test" and a file called "index.php" and add the following:

```php
<?php echo 'Hello World'; ?>
```

Now in your terminal, in that folder, run the following:

```bash
php -S localhost:3000
```

Now when you go to http://localhost:3000 you should see the hello world.

You can stop the server with Ctrl+C.

So you see, you could just install Laravel using Composer in any directory and just use the integrated server.


