# How to generate title slugs in Laravel

If you are not sure [what a slug exactly is](https://devdojo.com/devdojo/what-is-a-slug), you should go through this post here first:

[https://devdojo.com/devdojo/what-is-a-slug](https://devdojo.com/devdojo/what-is-a-slug)

There are many reasons why you would want to have a nice slug for your posts rather than accessing them via their ID, for example.

In this tutorial, you will learn how to use the title of your post and generate slugs for your Laravel blog or website!

All that you would need to follow along is a Laravel installation.

If you do not have a Laravel installation, you can follow the steps here on how to install Laravel with 1-Click also, get a **free $100 DigitalOcean credit**:

[https://devdojo.com/bobbyiliev/how-to-install-laravel-on-digitalocean-with-1-click](https://devdojo.com/bobbyiliev/how-to-install-laravel-on-digitalocean-with-1-click)

## Creating a slug in Laravel

To generate a slug, we can use one of the nice Helpers provided by Laravel, mainly the `Str::slug` method.

To do so, first, make sure to include the `Str` class to your Controller:

```
use Illuminate\Support\Str;
```

Then all that you need to do is to use the `Str::slug` method and pass in your title:

```
$slug = Str::slug('Your Awesome Blog Title', '-');
```

If you echo the `$slug` variable with `echo $slug`, the result will be the following:

```
your-awesome-blog-title
```

Of course, rather than passing a static string, you could pass the title from your POST request for example:

```
$slug = Str::slug($request->title, '-');
```

After that, you can store this in your database and later on retrieve your posts by slug rather than ID for example:

```
$post = Post::where('slug', $slug)->firstOrFail(); 
```

## Conclusion

This is pretty much it! Now you know how to create title slugs in your Laravel projects!

For more useful helpers, make sure to check the official documentation here:

[https://laravel.com/docs/8.x/helpers](https://laravel.com/docs/8.x/helpers)

[Originally posted here](https://devdojo.com/bobbyiliev/how-to-generate-title-slugs-in-laravel)