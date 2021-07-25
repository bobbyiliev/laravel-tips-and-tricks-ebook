# How to check your exact Laravel version

As of Laravel 6.x, it now follows [Semantic Versioning](https://semver.org/), which essentially means that the major framework releases are released every six months (February and August), and minor and patch releases may be released as often as every week. 

With that in mind your Laravel version could often change, so here are a couple of ways for you to find out the exact Laravel version that you have.

## Check your Laravel version with artisan

Laravel comes with a command-line interface called Artisan. 

Artisan provides a huge number of commands that help you manage and build your Laravel application.

In order to get your exact Laravel version you can just run the following command in the directory of your Laravel project:

```
php artisan --version
```

The output that you would get will look like this:

```
Laravel Framework 8.12.0
```

In the example above, we can see that we are Running Laravel `8.12.0`.

For more information, you can find the [official Artisan documentation here](https://laravel.com/docs/8.x/artisan).

## Check your Laravel version via your text editor

In case you do not have a terminal open, you might want to check your Laravel version via your text editor instead.

To do that, open the following file:

```
vendor/laravel/framework/src/Illuminate/Foundation/Application.php
```

Once you have the file open, just search for `VERSION`. The first constant in the `Application` class would be the Laravel version:

```
    /**
     * The Laravel framework version.
     *
     * @var string
     */
    const VERSION = '8.12.0';
```

## Conclusion

Those were just 2 quick was of **checking your exact Laravel version**.

If you are new to Laravel, I would recommend checking out this [Introduction to Laravel 7](https://www.youtube.com/watch?v=ZYDBQcnkj38&list=PL_UnIDIwT95Mn-Txakyt5x183aVXdve2R) free course by **DevDojo**.

Also, you could have a look at this course here on [how to build a blog using Laravel and Voyager](https://www.youtube.com/watch?v=RrhpbFCOlZ0&list=PLY7SzAmnEqp6bOl-AehM9dX3UKlxTjMVD). It shows you how to deploy and configure your own server with [DigitalOcean](https://www.youtube.com/redirect?q=https%3A%2F%2Fm.do.co%2Fc%2F2a9bba940f39&redir_token=eK6fiXPf8aOeA1k2lFWJ-mhGXSN8MTU5MzYwOTcwNUAxNTkzNTIzMzA1&event=video_description&v=RrhpbFCOlZ0) as well.

[Originally posted here](https://devdojo.com/bobbyiliev/how-to-check-your-exact-laravel-version)