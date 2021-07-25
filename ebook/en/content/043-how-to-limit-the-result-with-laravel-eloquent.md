# How to limit the result with Laravel Eloquent

The Eloquent ORM included with Laravel provides you with an easy way of interacting with your database. This simplifies all CRUD (Create, read, update, and delete) operations and any other database queries.

Laravel provides a lot of handy methods that you could use to work with your Eloquent collections. More often than not, when getting some results from your database, you would want to order them based on specific criteria. 

In this tutorial, **you will learn how to limit the results with Laravel Eloquent**!

Before you start, you would need to have a Laravel application up and running.

I will be using a DigitalOcean Ubuntu Droplet for this demo. If you wish, you can use my affiliate code to get [free $100 DigitalOcean credit](https://m.do.co/c/2a9bba940f39) to spin up your own servers!

If you do not have that yet, you can follow the steps from this tutorial on how to do that:

* [How to Install Laravel on DigitalOcean with 1-Click](https://devdojo.com/bobbyiliev/how-to-install-laravel-on-digitalocean-with-1-click)

Or you could use this awesome script to do the installation:

* [LaraSail](https://devdojo.com/episode/laravel-on-digital-ocean-with-larasail)

We will use a model called `Post` as an example in this tutorial.

## Limiting the result with pure SQL

In case that you were using pure SQL and wanted to limit the number of records returned by your query, you could use the `LIMIT` keyword, followed by the number of records that you would want to limit your result set to.

For example, let's say that we wanted to get only 5 posts from our posts table. The query would look like this:

```
SELECT * FROM posts LIMIT 5;
```

Now let's go through a couple of ways to do that with Laravel Eloquent.

## The `limit()` method

If we were to convert the above query to Eloquent, the syntax would look like this:

```
$posts = Post::limit(5)->get();
```

If you were to use [the `toSql` method to get the actual query](https://devdojo.com/bobbyiliev/how-to-get-the-laravel-query-builder-to-output-the-raw-sql-query) and `dd()` as follows:

```
dd(Post::limit(5)->toSql());
```

You would get the following output:

```
"select * from `posts` limit 5"
```

You could also specify an offset in case that you needed to with the `offset()` method.

An important thing that you need to keep in mind is that you could use the `limit()` method only with Eloquent, it does not work with collections.

Alternatively, you could use the `take()` method, which works with both Eloquent and collections.

## The `take()` method

I personally prefer to use the `limit()` method directly with Eloquent, but in some cases, it is handy to have the `take()` method on hand as well.

The syntax is more or less the same:

```
$posts = Post::take(20)->get();
```

Or if you already have your collection in place, you could again use the `take()` method as follows:

```
$posts = Post::get();
$posts->take(20);
```

## The `paginate()` method

In case that you are working on pagination, there is no need to use any of the above methods. Instead, you could just use the fantastic `paginate()` method that Laravel provides.

In your controller, you could specify the number of records that you would want to see on one page as follows:

```
$posts = Post::paginate(30)
```

And then, in your Blade view, you could use a `foreach` loop to loop through your posts and show the available pages as follows:

```
@foreach($posts as $post)
    <p>{{ $post->title }}</p>
@endforeach

{{ $posts ->links() }}
```

In the background, Laravel takes care of everything.

## Conclusion

If you are just getting started with Laravel, make sure to check out this introduction course here:

[Getting started with Laravel](https://devdojo.com/course/laravel-7-basics)

If you want to learn more about PHP in general, make sure to check out this [free PHP basics course here](https://devdojo.com/course/php-basics).

[Originally posted here](https://devdojo.com/bobbyiliev/how-to-limit-the-result-with-laravel-eloquent)