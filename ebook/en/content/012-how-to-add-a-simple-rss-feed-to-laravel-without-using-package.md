# How to add a simple RSS feed to Laravel without using a package

[RSS](https://en.wikipedia.org/wiki/RSS) stands for  Really Simple Syndication and is a feed that returns information in XML format.

Having an RSS feed would allow your users to track the latest posts on your website easily.

But having an RSS feed will also allow you to sign up for services like [http://daily.dev/](http://daily.dev/) or [http://dev.to](http://dev.to) and post your latest articles there automatically.

You can add an RSS feed to Laravel Application by using the [laravel-feed](https://github.com/spatie/laravel-feed). However, in this tutorial, I will show you how to do that easily without adding a whole package!

To get started, all that you need is a Laravel application.

If you don't have one, you can follow the steps here on [how to install Laravel on DigitalOcean with 1-Click](https://devdojo.com/bobbyiliev/how-to-install-laravel-on-digitalocean-with-1-click).

If you are new to DigitalOcean, you can use my referral link to get a free $100 credit so that you can spin up your own servers for free:

[Free $100 DigitalOcean credit](https://m.do.co/c/2a9bba940f39)

You would also need a model which you would work with. For this example, I will use my `Post` model that comes by default with the Laravel Voyager. And I will expose the latest posts from my **Laravel Voyager blog to my RSS feed**!

## Configuring RSS Controller

Let's start by creating a new controller called `RssFeedController`. You can do that with the following `php artisan` command:

```
php artisan make:controller RssFeedController
```

This will create a new controller for you, and it will add it to the `app/Http/Controllers/RssFeedController.php` directory.

After that, using your favorite text editor, open the file and add a new method called `feed` for example:

```
<?php

namespace App\Http\Controllers;
use Illuminate\Http\Request;
use TCG\Voyager\Models\Post;

class RssFeedController extends Controller
{
    public function feed()
    {
        $posts = Post::where('status', 'published')->
        orderBy('created_at', 'desc')->
        limit(50)->get();
        return response()->view('rss.feed', compact('posts'))->header('Content-Type', 'application/xml');

    }
}
```

Here is a quick rundown of the method:

* `use TCG\Voyager\Models\Post;`: First, we include the Voyager Post model. If you are not using Voyager, make sure to adapt this accordingly
* `public function index()`: Then specify the name of the method
* `$posts = Post::where('status', 'published')`: Then we define a new variable called `$posts` which would contain all of our `published` posts
* `orderBy('created_at', 'desc')`: We sort the posts so that we could get the newest on top
* `limit(50)->get();`: here we limit the results to 50 only so that we don't get too many posts back
* `return response()->view('rss.feed', compact('posts'))`:  Here we return the posts result to our `rss/feed.blade.php` view

With that, our Controller is ready! Next, we will configure our Blade view!

## Configuring your Blade view

Let's start by creating a folder called `rss` inside our `resources/views/` folder:

```
mkdir resources/views/rss
```

Then in that folder, create a file called `feed.blade.php`:

```
resources/views/rss/feed.blade.php
```

Then add the following content:

```
<?=
'<?xml version="1.0" encoding="UTF-8"?>'.PHP_EOL
?>
<rss version="2.0">
    <channel>
        <title><![CDATA[ DevDojo ]]></title>
        <link><![CDATA[ https://your-website.com/feed ]]></link>
        <description><![CDATA[ Your website description ]]></description>
        <language>en</language>
        <pubDate>{{ now() }}</pubDate>

        @foreach($posts as $post)
            <item>
                <title><![CDATA[{{ $post->title }}]]></title>
                <link>{{ $post->slug }}</link>
                <description><![CDATA[{!! $post->body !!}]]></description>
                <category>{{ $post->category }}</category>
                <author><![CDATA[{{ $post->user->username  }}]]></author>
                <guid>{{ $post->id }}</guid>
                <pubDate>{{ $post->created_at->toRssString() }}</pubDate>
            </item>
        @endforeach
    </channel>
</rss>
```

> Note: make sure to update the `<title>` and the description of your site!

With that, we define our RSS feed XML structure, and inside we use a `foreach` loop to print out all of our tutorials.

In case that you are not using Laravel Voyager, make sure to adjust the `$post->` properties so that they match your model!

## Configuring your Route

Finally, we need to create a new route and map it to our RSS Controller.

To do that, open the `routes/web.php` file and add the following line:

```
Route::get('feed', 'RssFeedController@feed');
```

Essentially with that, when someone visits `yoursite.com/feed`, they will get an RSS feed response back!

You can take a look at the following link as an example:

[RSS feed example](https://devdojo.com/feed)

## Conclusion

That is pretty much it. Now you have a fully functional RSS feed on your Laravel website!

Of course, you prefer to save some time, instead of adding the RSS functionality yourself, could use the [laravel-feed](https://github.com/spatie/laravel-feed) package instead!

[Originally posted here](https://devdojo.com/bobbyiliev/how-to-add-a-simple-rss-feed-to-laravel-without-using-package)**