# How to Get the Base URL in Laravel

Hardcoding the domain name in your Blade files or in your controllers is not a good practice. If you ever decided to change your website's domain name, you would have to manually go over all of your files and change the references of your website from the old domain to the new one.

This is why Laravel provides a clean way of doing this by only defining your application URL in one place and then accessing it via some handy Laravel helper functions.

In this tutorial, **you will learn how to get the Base URL in your Laravel application**!

Before you start, you would need to have a Laravel application up and running.

I will be using a DigitalOcean Ubuntu Droplet for this demo. If you wish, you can use my affiliate code to get [free $100 DigitalOcean credit](https://m.do.co/c/2a9bba940f39) to spin up your own servers!

If you do not have that yet, you can follow the steps from this tutorial on how to do that:

* [How to Install Laravel on DigitalOcean with 1-Click](https://devdojo.com/bobbyiliev/how-to-install-laravel-on-digitalocean-with-1-click)

Or you could use this awesome script to do the installation:

* [LaraSail](https://devdojo.com/episode/laravel-on-digital-ocean-with-larasail)

We will use a model called `Post` as an example in this tutorial.

## Access the Laravel Base URL

There are multiple ways of accessing the Laravel base URL. You could use one of the following approaches:

* The `url()` helper function:

```
echo url('');
```

You can also use this in your Blade template as follows:

```
{{  url('') }}
```

This will return the value of the `APP_URL` defined in your `.env` file:

```
https://domain.com
```

## Access the current URL in Laravel

The `url()` helper function comes with a lot of handy methods that you could use. Here are some of the most common ones:

* Get the current URL:

```
echo url()->current();
```

I can also be used in your Blade template directly as follows:

```
{{ url()->current() }}
```

* Get the current URL, including the GET parameters:

```
echo url()->full();
```

For more information about the `url()` helper, make sure to check out the official documentation [here](https://laravel.com/docs/8.x/helpers#method-url).

## Named routes

If you are using [named routes](https://devdojo.com/bobbyiliev/what-are-signed-routes-in-laravel-and-how-to-use-them), you could access the specific routes by using the `route()` helper.

> This is my preferred way of doing things as you would only be referencing the name of the route, so if the URL ever changes, you would not have to make any chances to your controllers and views as the routes would still be referenced by name rather than the specific URLs.

To access a named route, you could use the following:

```
echo route('posts');
```

This would check your routes file and return the correct route with name `posts`, e.g. `https://yourdomain.com/posts`.

You can also reference this directly in your Blade templates:

```
<a href="{{ route('posts') }}">My Posts</a>
```

The great thing about the `route` helper is that you can also pass parameters. So let's say that the route for your single posts accepts a `slug` to access a specific post. You could pass the slug to the route as follows:

```
{{ route('post', ['slug' => 'awesome-post-slug']) }}
```

Alternatively to the `url()` helper, you could use the URL facade.

## Access Assets URLs

In most cases, when referring to static assets stored in your public folder, like images, JavaScript and CSS files, the best approach is to use the `asset()` helper.

```
<img src="{{ asset('logo.png') }}" />
```

This will return `https://yourdomain.com/logo.png`, which is particularly handy if you are visiting the site from sub-pages like `/post/your-post` as if you don't specify the `asset()` helper, the logo would be loaded from `https://yourdomain.com/post/logo.png` which would result in 404. This is why I tend to use the `asset()` helper whenever possible.

## Conclusion

If you are just getting started with Laravel, make sure to check out this introduction course here:

[Getting started with Laravel](https://devdojo.com/course/laravel-7-basics)

If you want to learn more about PHP in general, make sure to check out this [free PHP basics course here](https://devdojo.com/course/php-basics).

[Originally posted here](https://devdojo.com/bobbyiliev/how-to-get-the-base-url-in-laravel)