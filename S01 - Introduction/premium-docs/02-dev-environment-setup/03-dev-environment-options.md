# Dev Environment Options

There are many ways to get PHP and Laravel setup on your local machine. In this video, we will look at some of the different ways to do so. You are free to use whichever method you prefer. In this course, I'm going to use Laravel Herd, so I'll show you how to get setup with that, but I'm also going to show you how to do a standard install of Laravel using Composer, which is a PHP package manager. 

Unless you're already using something else that you're happy with, Laravel Herd is what I would suggest. I think it is the easiest and most convient way to get both PHP and Laravel setup for MacOS and Windows. Even if you don't want to use the Herd features, it's still the easiest way to get PHP installed and configured. You can avoid the Herd sites folder and control panel alltogether if you want and just use the built in Artisan server, which I'll also demonstrate.

Herd comes configured with an NGINX server and a UI to manage your projects. If you want integrated databases like MySQL or Postgres, you do need the pro version, which I think is $99. However, you don't need it because you just install your database as a standalone, which is what we'll be doing.

In the next couple videos, I will show you how to get setup on both Mac and Windows. Before we do that, I just want to talk about some of the other options that you have.

## Manual Installation

Of course, you can manually install PHP is by itself. This is the most basic way to install PHP. The upside to this is that you have full control over the installation and can customize it to your liking. The downside is that you don't have the bells and whistles of a software suite. Also, you may run into some issues when it comes to PHP extensions and configuration.

The process of installing PHP is a little different depending on your operating system. You can use Homebrew on Mac, the installer on Windows and a package manager on Linux distros. 

## Laragon (Windows Only)

If you are on Windows, there is a tool called Laragon that will install PHP, Apache or NGINX, and MySQL for you. This is a great tool for beginners because it's easy to use and you don't have to worry about configuring anything. It's also great for advanced users because it's very powerful and has a lot of features. It's very fast and lightweight and it's easy to manage multuple versions of PHP if you need to. This is what I used before I learned about Herd.

## XAMPP (Windows, Mac, Linux)

XAMPP is an older suite that includes PHP, Apache, and MySQL for you. It's similar to Laragon but it's not as powerful. It's also a bit more difficult to use. I would recommend Laragon over XAMPP if you are on Windows. If you are on Mac or Linux, you can use XAMPP as well. Unfortunately, every time I have tried using XAMPP on Mac, I have run into issues but that could just be me.


## Laravel Homestead (Mac, Linux)

If you are on Mac or Linux and want to use Laravel, you can use Laravel Homestead. This is a Vagrant box, which is a virtual environment and it includes it's own install of PHP, Nginx, and MySQL. It's also obviously optimized for Laravel. The downside is that it's a little more difficult to use and it can take more resources to run. You also need to install Vagrant and VirtualBox. Vagrant is a tool that allows you to create and manage virtual machines. VirtualBox is the software that allows you to run virtual machines. I haven't used this tool very much, so I can't say much about it.

## Laravel Valet (Mac Only)

Laravel Valet is a development environment for macOS designed to be a minimal and fast alternative to using a full virtual machine setup. It's provided by Laravel for developers who prefer a more lightweight environment compared to Homestead. Again this tool is only available for Mac.

## Docker

Docker is a tool that allows you to run applications in containers. This is a great way to run PHP applications because you can run them in a container and not have to worry about installing PHP on your machine. This is great for development because you can run multiple versions of PHP at the same time. It's also great for production because you can run your application in a container and not have to worry about the environment. However, I definitely would not recommend this for beginners. It's a little more advanced and can be confusing. It's just something to think about for the future.

## Required PHP Extensions For Laravel

If you are going to be using Laravel, there are some PHP extensions that you will need enabled. You really only have to worry about this with a manual standalone installation. If you're using Herd or Laragon or something, these are already configured. With a manual install, you'll need to edit your `php.ini` file.

Here are the extensions you will need:

- **bcmath**: Provides support for arbitrary precision mathematics.
- **ctype**: Functions for character class checks and validation.
- **curl**: Enables transferring data with various protocols (e.g., HTTP, FTP).
- **fileinfo**: Detects file types and provides file information.
- **hash**: Provides hashing algorithms for data security (e.g., MD5, SHA-1).
- **mbstring**: Handles multi-byte string operations for different character encodings.
- **openssl**: Provides encryption and secure communication functions.
- **pdo**: Provides a consistent interface for database access using PDO (PHP Data Objects).
- **session**: Manages user sessions and session data.
- **tokenizer**: Provides functions for tokenizing PHP source code.
- **json**: Provides functions for encoding and decoding JSON data.


