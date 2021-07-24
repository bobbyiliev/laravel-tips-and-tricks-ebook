# How to Get Current Route Name in Laravel

[Laravel routes](https://www.youtube.com/watch?v=wEU3akZbZAM) allow you to map your URLs to specific functionality, for example, a method in a controller or directly to a specific Blade view. For example, if you visit `yourdomain.com/contact`, Laravel will return the contact page of your website.

In this tutorial, you will learn how to get your current route name in your Laravel application!

Before you start, you would need to have a Laravel application up and running.

I will be using a DigitalOcean Ubuntu Droplet for this demo. If you wish, you can use my affiliate code to get [free $100 DigitalOcean credit](https://m.do.co/c/2a9bba940f39) to spin up your own servers!

If you do not have that yet, you can follow the steps from this tutorial on how to do that:

* [How to Install Laravel on DigitalOcean with 1-Click](https://devdojo.com/bobbyiliev/how-to-install-laravel-on-digitalocean-with-1-click)

Or you could use this awesome script to do the installation:

* [LaraSail](https://devdojo.com/episode/laravel-on-digital-ocean-with-larasail)

## Get route name in Controller or Middleware

There are a few ways that you could get your Route's name in your Controller or Middleware.

You could use either the `Request` facade or the `Route` facade directly.

### Get route name using Route facade

To get your route's  name by using the `Route` facade, you could use the following:

* First include the `Route` facade to your controller:

```
use Illuminate\Support\Facades\Route;
```

* And then use the following in your method:

```
    public function yourMethodHere(){
        $routeName = Route::currentRouteName();
	dd($routeName);
    }
```

Or if you prefer note to include the facade, you could use the following instead:

```
    public function yourMethodHere(){
        $routeName = \Route::currentRouteName();
	dd($routeName);
    }
```

### Get route name using Request facade

Quite similar to using the `Route` facade, when using the `Request` facade you can get your current route's name by using the following:

```
    public function yourMethodHere(){
        $routeName = \Request::route()->getName();
        dd($routeName);
    }
```

## Get route name in Blade View

In some cases, you might want to check your current route name directly in your Blade view.

To do so, you could use the `Route` facade directly in your Blade view:

```
{{ Route::currentRouteName() }}
```

Or if you wanted to get your URI, you could also use the `request` function directly:

```
{{ request()->route()->uri }}
```

## Getting additional information about your route

In case that you wanted to get all of the information about the route you could call the `current()` method:

```
    public function yourMethodHere(){
        $routeInfo = \Route::current();
	dd($routeInfo);
    }
```

You would get the following information:

![Get Laravel Route Information](https://imgur.com/gYVY7x0.png)

You can then call specific properties like the `uri` for example:

```
    public function yourMethodHere(){
        $routeInfo = \Route::current()->url;
	dd($routeInfo);
    }
```

This would return only your URI!

## Conclusion

For more information on Laravel Routes, make sure to check this [video on how to add custom route files](https://devdojo.com/episode/laravel-custom-route-files)!

I strongly suggest checking out the official Laravel Documentation:

[https://laravel.com/docs/8.x/requests](https://laravel.com/docs/8.x/requests)

[Originally posted here](https://devdojo.com/bobbyiliev/how-to-get-current-route-name-in-laravel)