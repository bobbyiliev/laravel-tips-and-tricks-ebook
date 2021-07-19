# How to Create Response Macros in Laravel

Response macros allow you to create a custom response which you could later on re-use in different routes and controllers. 

This is quite beneficial in order to reduce code duplication.

You could actually built macros for other Laravel components as well, but in this tutorial, you will learn how to create a route macro for your Laravel application!

Before you start, you would need to have a Laravel application up and running.

I will be using a DigitalOcean Ubuntu Droplet for this demo. If you wish, you can use my affiliate code to get [free $100 DigitalOcean credit](https://m.do.co/c/2a9bba940f39) to spin up your own servers!

If you do not have that yet, you can follow the steps from this tutorial on how to do that:

* [How to Install Laravel on DigitalOcean with 1-Click](https://devdojo.com/bobbyiliev/how-to-install-laravel-on-digitalocean-with-1-click)

Or you could use this awesome script to do the installation:

* [LaraSail](https://devdojo.com/episode/laravel-on-digital-ocean-with-larasail)

## Creating a service provider

You could add your macro directly in the `app/Providers/AppServiceProvider.php` file under the `boot` method, but let's take this a step further and create our own service provider instead.

In order to create our service provider run the following command:

```
php artisan make:provider ResponseMacroServiceProvider
```

You will get the following output after running the command:

```
Provider created successfully.
```

This will generate a new file at:

```
app/Providers/ResponseMacroServiceProvider.php
```

After that, in order to register this new service provider open the `config/app.php` file and at the end of the `providers` array add the following:

```
    App\Providers\ResponseMacroServiceProvider::class,
```

With that in place we can move to the next step where we will create our response macro!

## Creating the Response Macro

Once we have the service provide in place it's time to build our response macro. 

With your favorite text editor open the `app/Providers/ResponseMacroServiceProvider.php` file and first include the `Response` facade:

```
<?php

namespace App\Providers;

use Illuminate\Support\Facades\Response;

use Illuminate\Support\ServiceProvider;
```

To keep things simple, our macro will expect a string as the input, then it will `base64` encode it and return the encoded string.

To do that, in the `boot()` method we will define our macro:

```
    public function boot()
    {
        Response::macro('bEncode', function ($value) {
            return Response::make(base64_encode($value));
        });
    }
```

The new macro is called `bEncode` for base64 encode.

## Using the Response Macro

Let's quickly test the new macro that we created by adding a  simple get route to the `routes/web.php` file:

```
Route::get('encode/{string}', function($string){
    return response()->bEncode($string);
});
```

Now if you were to visit the `/encode/some-string-here` route, you would get a response with the `some-string-here` string base64 encoded!

## Conclusion

Now you know how to create a macro in your Laravel application and use it in your routes and controllers.

For more information on Laravel macros, make sure to check out the official docs here:

[Laravel Response Macros](https://laravel.com/docs/8.x/responses#response-macros)

If you are just getting started with Laravel, make sure to check out this introduction course here:

[Getting started with Laravel](https://devdojo.com/course/laravel-7-basics)

[Originally posted here](https://devdojo.com/bobbyiliev/how-to-create-response-macros-in-laravel)