# How To Display HTML Tags In Blade With Laravel

Laravel is a great PHP framework that allows you to use Blade Templates for your frontend.

Blade is a very powerful templating engine provided with Laravel that does not restrict users from using plain PHP code in their views.

Blade view files that use the .blade.php file extension and are typically stored in the resources/views directory.

In this tutorial, you will learn how to display HTML in Blade with Laravel 8!

If you don't already have a Laravel application up and running, I suggest using a DigitialOcean Ubuntu Droplet. You can use my affiliate code to get [free $100 DigitalOcean credit](https://m.do.co/c/2a9bba940f39) to spin up your own servers!

If you do not have that yet, you can follow the steps from this tutorial on how to do that:

* [How to Install Laravel on DigitalOcean with 1-Click](https://devdojo.com/bobbyiliev/how-to-install-laravel-on-digitalocean-with-1-click)

Or you could use this awesome script to do the installation:

* [LaraSail](https://devdojo.com/episode/laravel-on-digital-ocean-with-larasail)

## Display HTML In Laravel Blade Views

First, you need to make sure your file uses the `.blade.php` file extension and is located in the `resources/views` folder. It should look something like this:

![index.blade.php](https://cdn.devdojo.com/images/november2020/125956057_361683805094042_391090211638948820_n.png)

By default you would use the following syntax `{{ $some_variable }}` to echo out the content of a specific variable in Blade. By default the `{{ }}` escapes the HTML tags. 

So let's say that you have a blog post with a `$post` collection which has some HTML elements in the `body` proerty, if you were to use the following:

```
<div>{{ $post->body }}</div>
```

All of the HTML tags would not be rendered as HTML but plain text:

![HTML tags in blade laravel](https://imgur.com/VRv7cTE.png)

If you don't want your HTML tags to be escaped then you should use `{!! !!}` just like this:

```
<div>{!! $post->body !!}</div>
```

Output:

![HTML rendered in blade laravel](https://imgur.com/pOb8xQW.png)

If you print out both and check the page source, you will see the following output:

![Laravel blade escape html elements](https://imgur.com/BaPKQrG.png)

```
&lt;h1&gt;Hello DevDojo&lt;/h1&gt;
<h1>Hello DevDojo</h1>
```

In the first case, you can see how the HTML elements were escaped, and in the second case where we use `{!! !!}` we got the actual HTML tags.

It is more secure to use `{{ }}` as it will strip out any unwanted tags, but there are still times where you might need to use `{!! !!}`.

## Conclusion

Blade templating is beneficial and can make your life easier.

If you want to learn more about Blade Templating, check out the official Laravel Documentation:

[https://laravel.com/docs/8.x/blade](https://laravel.com/docs/8.x/blade)

[Originally posted here](https://devdojo.com/bobbyiliev/how-to-display-html-tags-in-blade-with-laravel-8)