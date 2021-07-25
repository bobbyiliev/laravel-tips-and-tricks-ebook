# How to Define Custom ENV Variables in Laravel

If you have some experience with Linux, you are probably quite familiar with environment variables. In Linux, you could check the available environment variables with the `printenv` command. A way to define environment variables in Linux would be to use the `export` command followed by the variable that you want to define, for example: `export name=DevDojo`.

In this tutorial, you will learn a couple of ways of defining Laravel variables and accessing them in your application!

Before you start, you would need to have a Laravel application up and running.

I will be using a DigitalOcean Ubuntu Droplet for this demo. If you wish, you can use my affiliate code to get [free $100 DigitalOcean credit](https://m.do.co/c/2a9bba940f39) to spin up your own servers:

[![DigitalOcean Referral Badge](https://web-platforms.sfo2.digitaloceanspaces.com/WWW/Badge%203.svg)](https://www.digitalocean.com/?refcode=2a9bba940f39&utm_campaign=Referral_Invite&utm_medium=Referral_Program&utm_source=badge)

If you do not have that yet, you can follow the steps from this tutorial on how to do that:

* [How to Install Laravel on DigitalOcean with 1-Click](https://devdojo.com/bobbyiliev/how-to-install-laravel-on-digitalocean-with-1-click)

Or you could use this awesome script to do the installation:

* [LaraSail](https://devdojo.com/episode/laravel-on-digital-ocean-with-larasail)

## Defining a variable in `.env`

The `.env` file holds your env variables for your current environment. It is powered by the [DotEnv](https://github.com/vlucas/phpdotenv) Library.

As the `.env` file often holds sensitive information like API keys or database credentials, you should never commit it to Git and never push it to GitHub.

In order to define a new environment variable, you could use the following syntax: `VAR_NAME=YOUR_VALUE`. For example, let's say that you wanted to define your GitHub API key in there, the syntax would be the following:

```
GITHUB_API_KEY=your_api_key_here
```

In case that you have spaces in the value, it is best to use quotes:

```
NAME="Bobby Iliev"
```

## Accessing the env variable with `env()`

Once you've specified your environment variable in your `.env` file, you could then retrieve it in your application with the following helper function:

```
env('NAME')
```

The `env` helper function allows you to pass a default value in case that the env variable is not defined or does not have a value specified in the `.env` file:

```
env('NAME', 'DevDojo')
```

In the above example, if the `NAME` env variable is not defined, it will take the default value of `DevDojo`. 

## Accessing the env variable with `config()`

If you are [creating a new Laravel Package](https://devdojo.com/devdojo/how-to-create-a-laravel-package) or if you are building some specific functionality, it is pretty handy to define different configuration values in a configuration file stored in the `config` folder.

For example, let's say that we are building functionality that consumes the DigitalOcean API. What we can do is create a new file inside the `config` folder called `digitalocean.php`:

```
config/digitalocean.php
```

The content of the fill will be a single return statement that returns an array with different env configuration values:

```
<?php
  
return [
    'do_key' => env('DIGITALOCEAN_API_KEY', 'default_value_here'),
];
```

With that we would also need to define the actual value of the `DIGITALOCEAN_API_KEY` variable inside the `.env` file just as we did in the previous step:

```
DIGITALOCEAN_API_KEY='your_digitalocean_api_key_here'
```

After that, by using the `config` helper method, you could access the `do_key` value with the following syntax:

```
config('digitalocean.do_key')
```

Rundown of the syntax:

* `config('')`: First, we call the config helper
* Then, we specify the name of the configuration file inside the `config` folder. As we named the file `digitalocean.php` we need to just use `digitalocean`
* Finally separated with a dot we specify the value that we want to call

With that, you could also use the `php artisan config:cache` command to cache your env variables and give your website a slight speed boost.

> Important thing to keep in mind is that if you run the `config:cache` command, you will only be able to use the `env` helper inside configuration files in the `config` folder. And also, you need to have the `php artisan config:cache` command executed on every deployment.

## Conclusion

Now you know how to define custom variables in your Laravel application! For more information about the Laravel configuration, make sure to check out the official documentation here:

[https://laravel.com/docs/8.x/configuration](https://laravel.com/docs/8.x/configuration)

If you are just getting started with Laravel, make sure to check out this introduction course here:

[Introduction to Laravel](https://devdojo.com/course/laravel-7-basics)

[Originally posted here](https://devdojo.com/bobbyiliev/how-to-define-custom-env-variables-in-laravel)