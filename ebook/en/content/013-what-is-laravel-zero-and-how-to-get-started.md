# What is Laravel Zero and how to get started

[Laravel Zero](https://laravel-zero.com/) is an open-source PHP framework that can be used for creating console applications.

Laravel Zero is not an official Laravel package but was created by [Nuno Maduro](https://github.com/nunomaduro), who is also a Software Engineer at Laravel, so I have no doubts about the code quality.

This tutorial, will give you a quick introduction on how to get started with Laravel Zero and built a simple `Hello World` command-line application.

Before you get started, you would need to have PHP  and `composer` installed.

I will be using an Ubuntu server on DigitalOcean for this demo. If you are new to DigitalOcean, you can use my referral link to get a free $100 credit so that you can spin up your own servers for free:

**[Free $100 DigitalOcean credit](https://m.do.co/c/2a9bba940f39)**

Once you have a DigitalOcean account, you can follow the steps here on how to install `composer` and PHP:

* [How To Install and Use Composer on Ubuntu 20.04](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-composer-on-ubuntu-20-04)

## Installation

Before you start with the installation, make sure that you have the following PHP modules installed:

* `php-mbstring`
* `php-xml`

To check if you have those installed already, you can just run this command:

```
php -m
```

If you are following along and you've started an Ubuntu server, you can install the module with the following command:

```
sudo apt install php-mbstring php-xml
```

To create a new Laravel Zero project, you can run the following command:

```
composer create-project --prefer-dist laravel-zero/laravel-zero hello-world
```

> Note: You can change the `hello-world` part with the of your own name 

Now instead of `php artisan`, you will need to run `php application`, for example:

```
php application
```

Output:

```
  Application  unreleased

  USAGE: application <command> [options] [arguments]

  inspiring    Display an inspiring quote
  test         Run the application tests

  app:build    Build a single file executable
  app:install  Install optional components
  app:rename   Set the application name

  make:command Create a new command

  stub:publish Publish all stubs that are available for customization
```

If you want to, you could also change the name of your `application` by running the following command:

```
php application app:rename hell-world
```

This will rename the `application` executable to `hello-world` so from now on, instead of running `php application` you will need to run `php hello-world`:

```
php hello-world

  Hello-world unreleased

  USAGE: hello-world <command> [options] [arguments]

  inspiring    Display an inspiring quote
  test         Run the application tests

  app:build    Build a single file executable
  app:install  Install optional components
  app:rename   Set the application name

  make:command Create a new command

  stub:publish Publish all stubs that are available for customization
```

The content of the folder will look like this:

```
README.md
app
bootstrap
box.json
composer.json
composer.lock
config
hello-world
phpunit.xml.dist
tests
vendor
```

With that, we now have our Laravel Zero application ready. Next, let's dive into some of the available commands!

## Commands

In order to create a new command, you can run the following:

```
php hello-world make:command HelloWorldCommand
```

The output that you will get will be:

```
Console command created successfully.
```

This will generate a new file at: `app/Commands/HelloWorldCommand.php`.

Open the file with your favourite text editor and change the following things:

* Change this with the name of the command that you want to have:

```
protected $signature = 'command:name';
```

* Change this with the description of your command:

```
 protected $description = 'Command description';
```

* Inside the `handle()` method you can add your logic, in our case we could just output a simple message:

```
    public function handle()
    {
        echo 'Hello World';
    }
```

If you've ever created a [custom artisan command](https://www.digitalocean.com/community/questions/how-do-i-create-a-simple-artisan-command-in-laravel), you would probably find the process very similar.

## Configuration

The configuration files for your Laravel Zero application are stored inside the `config` directory.

By default there are two files in there:

* `app.php`: it contains some information for your application
* `commands.php`: you can configure the list with the default commands in that file

If you add a new file inside the `config` directory, it will be automatically registered. For example, let's add a file called `hello.php`:

```
touch config/hello.php
```

Then add the following content:

```
<?php
return [
    'greeting' => 'Hello World!',
];
```

You will also be able to access it with `config('hello.greeting')`, as an example you can update the `handle()` method of your test command that you created in the last step to:

```
    public function handle()
    {
        echo config('hello.greeting');
    }
```

If you want to have the `.env` file back, you can install the `Dotenv` addon by running the following command:

```
php hello-world app:install dotenv
```
Next, we will go through some more of the available addons for Laravel Zero!

## Addons

Out of the box Laravel Zero is quite stripped so you don't have any uncessacry code in your application, that way you can keep it as light as possible.

You can use the `app:install` command in order to include an addon.

To get a list of the available addons, just run:

```
php hello-world app:install
```

You will see the following output:

```
 Laravel Zero - Component installer:
  [console-dusk ] Console Dusk: Browser automation
  [database     ] Eloquent ORM: Database layer
  [dotenv       ] Dotenv: Loads environment variables from ".env"
  [http         ] Http: Manage web requests using a fluent HTTP client
  [log          ] Log: Robust logging services
  [logo         ] Logo: Display app name as ASCII logo
  [menu         ] Menu: Build beautiful CLI interactive menus
  [queue        ] Queues: Unified API across a variety of queue services
  [schedule-list] Schedule List: List all scheduled commands.
  [self-update  ] Self-update: Allows to self-update a build application
```

You can use the interactive menu to choose an addon and install it!

In this post I will through a couple!

### Database

In order to include the Laravel's Eloquent component, you need to run the following command:

```
php hello-world app:install database
```

> Note: don't forget to change the `hello-world` part with the name of your application.

In the background the `app:install` command uses composer, so the output that you would see will be quite familiar for you if you've ever used composer:

```
Installing database component...
Require package via composer: loading...
Do not run Composer as root/super user! See https://getcomposer.org/root for details
./composer.json has been updated
Loading composer repositories with package information
Updating dependencies (including require-dev)
Package operations: 1 install, 0 updates, 0 removals
  - Installing illuminate/database (v8.8.0): Downloading (100%)
```

This will add a new config file for you at `config/database.php` where you can configure your database details. By default it uses SQLite so you don't need to make any changes unless you want to use a different SQL engine.

Once Database the addon has been installe, you can use it just as you would use Elequent in Laravel!

Usage:

```
php hello-world make:migration create_users_table
php hello-world migrate

use DB;

$users = DB::table('users')->get();
```

### Logging

In order to install the Logging addon, you just need to run:

```
php <your-app-name> app:install log
```

This will include the Laravel logging service into your Laravel Zero project!

The usage is as follows:

```
use Log;

Log::emergency($message);
Log::alert($message);
Log::critical($message);
Log::error($message);
Log::warning($message);
Log::notice($message);
Log::info($message);
Log::debug($message);
```
## Building the application

Once you are ready with building the application, you can run the following command to build a single file executable:

```
php hello-world app:build
```

This will ask you for your build version and it will generate a single executable inside the `builds` folder!

## Conclusion

This is pretty much it! Now you know how to use Laravel Zero and build cool command-line applications!

For more information, make sure to checkout the official documentation here:

[https://laravel-zero.com/docs/](https://laravel-zero.com/docs/)

If you like the project, make sure to star it on [GitHub](https://github.com/laravel-zero/laravel-zero).

[Originally posted here](https://devdojo.com/bobbyiliev/what-is-laravel-zero-and-how-to-get-started)