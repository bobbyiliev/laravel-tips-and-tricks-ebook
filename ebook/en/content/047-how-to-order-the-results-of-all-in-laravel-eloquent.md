# How to Order the Results of all() in Laravel Eloquent

The Eloquent ORM included with Laravel provides you with an easy way of interacting with your database. This simplifies all CRUD (Create, read, update, and delete) operations and any other database queries.

Laravel provides a lot of handy methods that you could use to work with your Eloquent collections. More often than not, when getting some results from your database, you would want to order them based on specific criteria. 

In this tutorial, **you will learn how to order the results of `all()` in Laravel Eloquent**!

Before you start, you would need to have a Laravel application up and running.

I will be using a DigitalOcean Ubuntu Droplet for this demo. If you wish, you can use my affiliate code to get [free $100 DigitalOcean credit](https://m.do.co/c/2a9bba940f39) to spin up your own servers!

If you do not have that yet, you can follow the steps from this tutorial on how to do that:

* [How to Install Laravel on DigitalOcean with 1-Click](https://devdojo.com/bobbyiliev/how-to-install-laravel-on-digitalocean-with-1-click)

Or you could use this awesome script to do the installation:

* [LaraSail](https://devdojo.com/episode/laravel-on-digital-ocean-with-larasail)

We will use a model called `Post` as an example in this tutorial.

## Ordering the results on a query level

Before we cover how to sort the results on a collection level, let's first briefly cover how we would sort the results on a query level.

Let's say that we wanted to sort all of our posts by name. When getting the results from the database, we could use the `orderBy` method followed by the `get` method: 

```
$posts = Post::orderBy('name')->get();
```

If you added the `toSql()` method instead of the `get()` and used `dd` to print out the output as follows: 

```
$posts = Post::orderBy('name')->toSql();
dd($posts);
```

The actual query, you would get the following output:

```
"select * from `posts` order by `name` asc";
```

So as you can see, the `orderBy` method actually represents the `ORDER BY` function in SQL.

By default, Eloquent will order by ascending, but you could also order by descending by using the `orderByDesc()` method:

```
$posts = Post::orderByDesc('name')->get();
```

To learn more about SQL, you can check out this [free eBook on how to get started with SQL here](https://github.com/bobbyiliev/introduction-to-sql).

However, if you use `all()` rather than `get()` you would first get all of the entries from your Database and store them in a collection. And once you have the collection ready, you would need to use the available [Laravel collection methods](https://laravel.com/docs/master/collections#available-methods) rather than the eloquent methods.

## Ordering the results on a collection level with `all()`

To summarize the above, you can use the Eloquent methods while building your query, this would be a more efficient way of sorting your results. But you could also use the available collection methods to order the contents of a collection too.

This means that at a collection level, you could use the available `sortBy` method rather than the `orderBy` method, which is available at the query level.

Similar to the Eqluent methods, you can sort by ascending order using the `sortBy` method and sort by descending order using the `sortByDesc` method:

* Ascending:

```
$posts = Post::all();

$posts->sortBy("name");
```

* Descending:

```
$posts = Post::all();

$posts->sortByDesc("name");
```

Alternatively, you could chain the method too:

```
// Ascending
$posts = Post::all()->sortBy("name");

//Descending
$posts = Post::all()->sortByDesc("name");
```

Whenever I have the chance, I would use the `orderBy` method, but it is still quite handy to be able to easily order your results on a collection level.

## Conclusion

If you are just getting started with Laravel, make sure to check out this introduction course here:

[Getting started with Laravel](https://devdojo.com/course/laravel-7-basics)

If you want to learn more about PHP in general, make sure to check out this [free PHP basics course here](https://devdojo.com/course/php-basics).

[Originally posted here](https://devdojo.com/bobbyiliev/how-to-order-the-results-of-all-in-laravel-eloquent)