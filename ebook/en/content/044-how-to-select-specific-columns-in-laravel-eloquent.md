# How to Select Specific Columns in Laravel Eloquent

The Eloquent ORM included with Laravel provides you with an easy way of interacting with your database. This simplifies all CRUD (Create, read, update, and delete) operations and any other database queries.

In some specific cases you might not want to get all of the columns from a specific table but just one or some of them.

In this tutorial, **you will learn how to select specific columns in Laravel eloquent**!

Before you start, you would need to have a Laravel application up and running.

I will be using a DigitalOcean Ubuntu Droplet for this demo. If you wish, you can use my affiliate code to get [free $100 DigitalOcean credit](https://m.do.co/c/2a9bba940f39) to spin up your own servers!

If you do not have that yet, you can follow the steps from this tutorial on how to do that:

* [How to Install Laravel on DigitalOcean with 1-Click](https://devdojo.com/bobbyiliev/how-to-install-laravel-on-digitalocean-with-1-click)

Or you could use this awesome script to do the installation:

* [LaraSail](https://devdojo.com/episode/laravel-on-digital-ocean-with-larasail)

## Select specific columns with SQL only

Let's say that we had a table called users with the following columns: `name, username, age, email, phone`.

If you wanted to get all of the information from that table with only SQL the query would look like this:

```
SELECT * FROM users WHERE username = 'bobbyiliev';
```

However, if you wanted to get only, let's say, the age of the user, you would need to change the `*` symbol with the name of the column:

```
SELECT age FROM users WHERE username = 'bobbyiliev';
```

If you wanted to get two columns, you would divide them by a comma:

```
SELECT name,age FROM users WHERE username = 'bobbyiliev';
```

Now that we know how to do this with SQL only, let's learn how we can achieve this with Laravel.

## Select specific columns with Laravel Eloquent

Let's say that we already have our `User` model in place. To get all of the columns from the `users` table, we would use the following:

```
$user = User::where('username', 'bobbyiliev')->get();
```

However, if you wanted to get only a specific column, you could pass it as an argument to the `get()` method. 

The argument needs to be an **array containing a list of the columns that you want to get**:

```
$user = User::where('username', 'bobbyiliev')->get(['name']);
```

You could do the same with the `first()` and `all()` methods as well:

```
$user = User::where('username', 'bobbyiliev')->first(['name', 'age']);
```

If you wanted to get the value of a single column, you could use the following:

```
User::where('username', 'bobbyiliev')->first(['name'])->name;
```

However, I would personally first [check if there are any entires that match the condition](https://devdojo.com/bobbyiliev/how-to-check-if-a-record-exists-with-laravel-eloquent) and then get the property.

## Conclusion

If you are just getting started with Laravel, make sure to check out this introduction course here:

[Getting started with Laravel](https://devdojo.com/course/laravel-7-basics)

If you want to learn more about SQL in general make sure to check out this [free introduction to SQL eBook here](https://github.com/bobbyiliev/introduction-to-sql).

[Originally posted here](https://devdojo.com/bobbyiliev/how-to-select-specific-columns-in-laravel-eloquent)