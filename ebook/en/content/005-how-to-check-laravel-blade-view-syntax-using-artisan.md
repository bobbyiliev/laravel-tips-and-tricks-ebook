# How to check Laravel Blade View Syntax using artisan

The Laravel community has been growing exponentially, and there are a lot of fantastic packages out there. I recently came across a Laravel package that provides an artisan command to check the syntax of your blade templates.

In this tutorial, I will show you how to use the [Laravel Blade Linter package](https://github.com/Magentron/laravel-blade-lint) to check your blade views syntax!

Before getting started, you need to have a Laravel project up and running.

You can use the following referral link to get free $100 credit that you could use to deploy your servers and test the guide yourself:

[DigitalOcean $100 Free Credit](https://m.do.co/c/2a9bba940f39)

After that, you can follow the steps on [How to Install Laravel on DigitalOcean with 1-Click here](https://devdojo.com/bobbyiliev/how-to-install-laravel-on-digitalocean-with-1-click)!

## Installation

```
composer require magentron/laravel-blade-lint
```

## Testing

Once you have the package installed, in order to test your Blade syntax, you need to run the following command:

```
php artisan blade:lint
```

If you don't have any errors, you would see the following output:

```
All Blade templates OK!
```

On another note, if there are any issues anywhere in your blade files, you would get an error like this one:

```
PHP Parse error:  syntax error, unexpected ':', expecting '(' in /var/www/html/resources/views/welcome.blade.php on line 103
Found 1 errors in Blade templates!
```

In my case, it tells me that I have a syntax error on line 103 in my `welcome.blade.php` file.

If you don't want to check all of your views, you can specify the path to a specific directory:

```
php artisan blade:lint resources/views/blog
```

## Conclusion

The Laravel Blade Linter is a great package that can help you avoid errors before pushing your code to production!

If you like the package, make sure to contribute at on [Github](https://github.com/Magentron/laravel-blade-lint)!

[Originally posted here](https://devdojo.com/bobbyiliev/how-to-check-laravel-blade-view-syntax-using-artisan)