# How to get the Laravel Query Builder to Output the Raw SQL Query

The Eloquent ORM included with Laravel provides you with an easy way of interacting with your database. This simplifies all CRUD (Create, read, update, and delete) operations and any other database queries.

When troubleshooting problems with the Laravel query builder, you might want to see the actual SQL query that is being executed for debugging purposes.

Here are a couple of quick ways that you could use to quickly get the query Builder to output its raw SQL query as a string!

Before you begin, you need to have Laravel installed. 

If you do not have that yet, you can follow the steps from this tutorial on how to do that:

* [How to Install Laravel on DigitalOcean with 1-Click](https://devdojo.com/bobbyiliev/how-to-install-laravel-on-digitalocean-with-1-click)

Or you could use this awesome script to do the installation:

* [LaraSail](https://devdojo.com/episode/laravel-on-digital-ocean-with-larasail)

You would also need to have a model ready that you would like to use. For example, I have a small blog with a `posts` table and `Post` model that I would be using.

## The `toSql()` method

When I first started using Laravel, I was amazed by how convenient and handy the Eloquent ORM and how much it speeds up the whole development process.

You can use the `toSql()` method to get the plain SQL representation of your query. 

As an example, let's say that we want to get all posts that are published. If we had to write this in pure SQL, it would look like this:

```
SELECT * FROM posts WHERE status='published';
```

And here is how we would do this with Laravel:

```
$posts = Post::where('status', 'published')->get();
```

In order to use the `toSql()` method, you could just change the `get()` part in the above query with `toSql()`:

```
$posts = Post::where('status', 'published')->toSql();
```

Then you could use `dd()` to dump the output on the screen:

```
dd($posts);
```

You will see the following output:

![Laravel toSql example](https://imgur.com/7V4itEc.png)

```
"select * from `posts` where `status` = ?"
```

As you can see the binding in this case is represented as `?`, to get the bindings you could use the `getBindings()` method:

```
$posts = Post::where('status', 'published')->getBindings();
dd($posts);
```

## Laravel Debugbar

I love the `toSql()` method, but in some cases having to manually add this across your application while debugging could be intimidating. 

This is why, as an alternative, you could use the [Laravel Debugbar Package](https://github.com/barryvdh/laravel-debugbar).

It would give you a really nice bar with a lot of useful debug information.

To add the package to your application, you could use the following composer command:

```
composer require barryvdh/laravel-debugbar --dev
```

> Note the `--dev` flag, it is crucial as you don't want to have the debug bar available in your production environment.

For more information on how to use the debug bar, make sure to check out the documentation [here](https://github.com/barryvdh/laravel-debugbar).

## Conclusion

The `toSql()` method could be very handy when troubleshooting problems with your eloquent queries!

If you are just getting started with Laravel, I would recommend going through [this Laravel introduction course](https://devdojo.com/course/laravel-7-basics).

[Originally posted here](https://devdojo.com/bobbyiliev/how-to-get-the-laravel-query-builder-to-output-the-raw-sql-query)