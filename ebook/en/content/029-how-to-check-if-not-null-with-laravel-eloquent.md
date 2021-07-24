# How to check 'if not null' with Laravel Eloquent

The Eloquent ORM included with Laravel provides you with an easy way of interacting with your database. This simplifies all CRUD (Create, read, update, and delete) operations and any other database queries.

In this tutorial, you will learn how to check if the value of a specific column is `NULL` or not with Laravel Eloquent!

Before you start, you would need to have a Laravel application up and running.

I will be using a DigitalOcean Ubuntu Droplet for this demo. If you wish, you can use my affiliate code to get [free $100 DigitalOcean credit](https://m.do.co/c/2a9bba940f39) to spin up your own servers!

If you do not have that yet, you can follow the steps from this tutorial on how to do that:

* [How to Install Laravel on DigitalOcean with 1-Click](https://devdojo.com/bobbyiliev/how-to-install-laravel-on-digitalocean-with-1-click)

Or you could use this awesome script to do the installation:

* [LaraSail](https://devdojo.com/episode/laravel-on-digital-ocean-with-larasail)

## Check if null: `whereNull`

Let's have the following example and let's say that we have a Users table, and we want to get a list of all users that have not specified their last name, for example.

In case we were using pure SQL, the query would look like this:

```
SELECT *
FROM users
WHERE last_name IS NULL;
```

> Notice the `IS NULL` expression at the end

The above query would return all of the users in your database where their last name is set to `NULL`.

Laravel Eloquent provides a handy method called `whereNull`, which you could use to verify if a specific value of a given column is NULL. 

So in this case, the above example would look like this with Eloquent:

```
$users = User::whereNull('last_name')
                    ->get();
```

Or in case that you prefer using the `DB` facade it would look like this:

```
$users = DB::table('users')
                    ->whereNull('last_name')
                    ->get();
```

## Check if not null: `whereNotNull`

Let's have a similar example, but in this case, we want to get all users that have specified their last names.

In pure SQL, we would use the `IS NOT NULL` condition, and the query would look like this:

```
SELECT *
FROM users
WHERE last_name IS NOT NULL;
```

The equivalent to the `IS NOT NULL` condition in Laravel Eloquent is the `whereNotNull` method, which allows you to verify if a specific column's value **is not `NULL`**.

So in this case, by using the `whereNotNull` method, the above example would look like this with Eloquent:

```
$users = User::whereNotNull('last_name')
                  ->get();
```

And again, in case that you prefer using the `DB` facade it would look like this:

```
$users = DB::table('users')
                    ->whereNotNull('last_name')
                    ->get();
```

## Conclusion

For more information and useful tips on Laravel Eloquent, make sure to check this tutorial here:

[Laravel Eloquent Make](https://devdojo.com/tnylea/laravel-eloquent-make)

I strongly suggest checking out the official Laravel Documentation:

* [Laravel Eloquent](https://laravel.com/docs/8.x/eloquent)

[Originally posted here](https://devdojo.com/bobbyiliev/how-to-check-if-not-null-with-laravel-eloquent)