# How to Set a Variable in Laravel Blade Template

The Blade templating engine has been a real game-changer for me. Blade makes it working with PHP and HTML a breeze. It allows you to use plain PHP code directly in your template.

In most cases, you will pass your variables from your controller to your Blade views, but you might want to set a variable directly in your Blade view in some cases.

In this tutorial, **you will learn how to set a variable in your Laravel Blade Template directly**!

Before you start, you would need to have a Laravel application up and running.

I will be using a DigitalOcean Ubuntu Droplet for this demo. If you wish, you can use my affiliate code to get [free $100 DigitalOcean credit](https://m.do.co/c/2a9bba940f39) to spin up your own servers!

If you do not have that yet, you can follow the steps from this tutorial on how to do that:

* [How to Install Laravel on DigitalOcean with 1-Click](https://devdojo.com/bobbyiliev/how-to-install-laravel-on-digitalocean-with-1-click)

Or you could use this awesome script to do the installation:

* [LaraSail](https://devdojo.com/episode/laravel-on-digital-ocean-with-larasail)

## Returning a variable from a controller

You could pass variables to the `view` helper function directly from your controller or route in some cases.

The syntax is the following:

```
return view('dashboard', ['name' => 'Bobby']);
```

The above will return the `dashboard.blade.php` view, and a variable called `$name` with the value of `Bobby` will be available so you could call it like this in your view:

```
<p> Welcome on board {{ $name }}!</p<
```

By default, this will escape all HTML tags, but in case that you needed to render HTML tags, you could follow the steps on how to do that here:

* [How To Display HTML Tags In Blade With Laravel](https://devdojo.com/bobbyiliev/how-to-display-html-tags-in-blade-with-laravel-8)

Alternatively, you could use the `compact` helper function to pass multiple variables from your controller to your view:

```
$name = 'Bobby';
$twitter = 'bobbyiliev_';

return view('dashboard', compact('name', 'twitter'));
```

Now that we've got this covered, here is how you could define a variable directly in your Blade template rather than passing it from your controller.

## Setting variables in Laravel Blade Template

As you could use plain PHP directly in your Blade template, all that you need to do in order to define a new variable is to use the following syntax in your view:

```
@php
    $name = "Bobby";
@endphp

<p>Hi there {{ $name }} 👋</p>
```

Thanks to the `@php` directive, you could actually write pure PHP directly in your view. Even though that, it would probably be better to keep any complex logic in your controller. Still, in some cases, it is super handy to have this as an option.

Alternatively, you could actually use general PHP opening and closing tags, but I prefer to stick to the Blade PHP block instead:

```
<?php 
    $name = "Bobby"; 
?>
```

## Conclusion

If you are just getting started with Laravel, make sure to check out this introduction course here:

[Getting started with Laravel](https://devdojo.com/course/laravel-7-basics)

If you want to learn more about PHP in general, make sure to check out this [free PHP basics course here](https://devdojo.com/course/php-basics).

[Originally posted here](https://devdojo.com/bobbyiliev/how-to-set-a-variable-in-laravel-blade-template)