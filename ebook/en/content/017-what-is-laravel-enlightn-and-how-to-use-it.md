# What is Laravel Enlightn and how to use it

The [Laravel Enlightn](https://www.laravel-enlightn.com/) was developed by [Miguel Piedrafita](https://twitter.com/m1guelpf) and [Paras Malhotra ](https://twitter.com/parasume).

It is an `artisan` command-line tool that checks your code and provides you with actionable recommendations on improving your application's performance, security & more. 

The [Laravel Enlightn](https://www.laravel-enlightn.com/) comes with a free community version, which includes 60 checks, and also there is a Pro version for solo developers or businesses and teams. You can check out the pricing [here](https://www.laravel-enlightn.com/#pricing).

Miguel announces the release today (14 Jan 2021) via this tweet [here](https://twitter.com/m1guelpf/status/1349627536972640258).

In this tutorial, you will learn how to install and use Laravel Enlightn to scan your website!

Before you start, you would need to have a Laravel application up and running.

I will be using a DigitalOcean Ubuntu Droplet for this demo. If you wish, you can use my affiliate code to get [free $100 DigitalOcean credit](https://m.do.co/c/2a9bba940f39) to spin up your own servers!

If you do not have that yet, you can follow the steps from this tutorial on how to do that:

* [How to Install Laravel on DigitalOcean with 1-Click](https://devdojo.com/bobbyiliev/how-to-install-laravel-on-digitalocean-with-1-click)

Or you could use this awesome script to do the installation:

* [LaraSail](https://devdojo.com/episode/laravel-on-digital-ocean-with-larasail)

## Installation

In order to install Laravel Enlightn, all that you need to do is run the following composer command:

```
composer require enlightn/enlightn
```

This will install the free open source Enlightn version. If you've purchased the premium one, make sure to follow the installation steps for the Pro package [here](https://www.laravel-enlightn.com/docs/getting-started/installation.html#installing-enlightn-pro).

Once you have the package installed, you can publish the assets as normal with the `artisan vendor:publish` command:

```
php artisan vendor:publish --tag=enlightn
```

To check if Enlightn was installed, you can use the following command:

```
php artisan  | grep enlightn
```

Output:
```
  enlightn                              Enlightn your application!
```

## Configuration

Once you've installed the package and published the assets, you can find the configuration file at:

```
config/enlightn.php
```

In that file, you can configure which checks you want to be executed.

The Enlightn Pro version comes with 120 checks, whereas the free community version comes with 60.

## Usage

All that you need to do in order to run Enlightn is to use the following `artisan` command:

```
php artisan enlightn
```

If you are using the free version, this will trigger the 60 checks against your code, which would analyze your code's performance, security, and reliability!

Output:

```
    ______      ___       __    __
   / ____/___  / (_)___ _/ /_  / /_____
  / __/ / __ |/ / / __  / __ |/ __/ __ |
 / /___/ / / / / / /_/ / / / / /_/ / / /
/_____/_/ /_/_/_/\__, /_/ /_/\__/_/ /_/
                /____/


Please wait while Enlightn scans your codebase...

|------------------------------------------
| Running Performance Checks
|------------------------------------------

Check 1/60: A proper cache driver is configured. Passed

Check 2/60: Your application caches compiled assets for improved performance. Passed

Check 3/60: Aggregation is done at the database query level rather than at the Laravel Collection level. Passed

Check 4/60: Application config caching is configured properly. Passed

Check 5/60: Your application does not use the debug log level in production. Passed

Check 6/60: Dev dependencies are not installed in production. Passed
...
```

You would see a lot of valuable feedback that will help you patch and optimize your code. This could protect your website against malicious attacks.

## Analyzing the output

If your code passes a certain check, you will get a green messaged next to the check saying `Passed`.

However, if a specific check fails, you will get a summary of the problem.

For example, I'm running the script against a new SaaS that I'm working on based on [Laravel Wave](https://wave.devdojo.com). Thanks to Laravel Enlightn, I've noticed the following problem with one of the methods that I've created:

```
Check 30/60: Your application does not contain invalid method calls. Failed
Your application seems to contain invalid method calls to methods that either does not exist or do not match the method signature or scope.
At /app/Http/Livewire/ServiceRatings.php: line(s): 72 and 88.
Documentation URL: https://www.laravel-enlightn.com/docs/reliability/invalid-method-call-analyzer.html
```

The output informs me where the problem is, what is wrong, and where to find more information about it.

This allows me to patch the problem before I push my code to production!

Here is another great finding where I've seen to have used an undefined variable in one of my controllers:

```
Check 39/60: Your application does not reference undefined variables. Failed
Your application seems to reference undefined variables.
At /app/Http/Controllers/ServiceController.php: line(s): 67 and 68.
Documentation URL: https://www.laravel-enlightn.com/docs/reliability/undefined-variable-analyzer.html
```

This will help you prevent such unecessary mistakes in the future.

The tool also scans your environment setup like PHP, MySQL, etc., and gives you suggestions about possible optimizations.

## Conclusion

I strongly recommend checking out Laravel Enlightn as it is an awesome tool that could help you protect and optimize your Laravel application.

After testing the tool on a couple of the Laravel projects that I work on, I could admit that this tool is going to be a game-changer for me, and I will definitely use it for all of my projects from now on!

For more information, make sure to check out the official documentation here:

[Laravel Enlightn](https://www.laravel-enlightn.com/docs/getting-started/installation.html)

[Originally posted here](https://devdojo.com/bobbyiliev/what-is-laravel-enlightn-and-how-to-use-it)