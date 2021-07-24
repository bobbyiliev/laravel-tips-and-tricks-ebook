# How to Delete All Entries in a Table Using Laravel Eloquent

The Eloquent ORM included with Laravel provides you with an easy way of interacting with your database. This simplifies all CRUD (Create, read, update, and delete) operations and any other database queries.

Laravel provides a lot of handy methods that you could use to work with your Eloquent collections. More often than not, when getting some results from your database, you would want to order them based on specific criteria. 

In this tutorial, **you will learn how to delete/truncate all entries in a table using Laravel Eloquent**!

Before you start, you would need to have a Laravel application up and running.

I will be using a DigitalOcean Ubuntu Droplet for this demo. If you wish, you can use my affiliate code to get [free $100 DigitalOcean credit](https://m.do.co/c/2a9bba940f39) to spin up your own servers!

If you do not have that yet, you can follow the steps from this tutorial on how to do that:

* [How to Install Laravel on DigitalOcean with 1-Click](https://devdojo.com/bobbyiliev/how-to-install-laravel-on-digitalocean-with-1-click)

Or you could use this awesome script to do the installation:

* [LaraSail](https://devdojo.com/episode/laravel-on-digital-ocean-with-larasail)

We will use a model called `Post` as an example in this tutorial.

## Using `truncate` to delete all entries from a table

If we were writing pure SQL, to delete all entries from a table, we could use the `TRUNCATE` function as follows:

```
TRUNCATE users;
```

This will basically truncate the entire table, and it would also reset the auto-incrementing IDs to zero.

To do the same thing with Eloquent, we could use the `DB` facade as follows:

```
DB::table('posts')->truncate();
```

Alternatively, you could call the `truncate()` method directly on your model:

```
Post::truncate();
```

## Delete all entries using the `delete()` method

If you wanted to delete only some specific entries, you could first get the entries as follows:

```
Post::query()->delete();
```

The benefit of using `delete()` rather than using `truncate()` is that you could specify some conditions so that you could only delete specific entries and not all of them:

```
Post::where('active', false)->delete();
```

Alternatively, you could also use the `DB` facade rather than calling the model directly:

```
DB::table('posts')->delete();

DB::table('posts')->where('active', false)->delete();
```

The main benefit of using `turncate` is that the auto-increment IDs will also be rest.

## Conclusion

If you are just getting started with Laravel, make sure to check out this introduction course here:

[Getting started with Laravel](https://devdojo.com/course/laravel-7-basics)

If you want to learn more about PHP in general, make sure to check out this [free PHP basics course here](https://devdojo.com/course/php-basics).

[Originally posted here](https://devdojo.com/bobbyiliev/how-to-delete-all-entries-in-a-table-using-laravel-eloquent)