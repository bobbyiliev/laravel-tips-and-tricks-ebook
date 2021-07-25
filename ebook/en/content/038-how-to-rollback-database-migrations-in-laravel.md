# How to Rollback Database Migrations in Laravel

Laravel comes with many convenient tools out of the box, which makes your life as a developer much more enjoyable.

One of the best Laravel features is the database migrations which essentially allow you to version control your database!

In this tutorial, you will learn how to rollback your database migrations in Laravel if you ever have to do so!

Before you start, you would need to have a Laravel application up and running.

I will be using a DigitalOcean Ubuntu Droplet for this demo. If you wish, you can use my affiliate code to get [free $100 DigitalOcean credit](https://m.do.co/c/2a9bba940f39) to spin up your own servers!

If you do not have that yet, you can follow the steps from this tutorial on how to do that:

* [How to Install Laravel on DigitalOcean with 1-Click](https://devdojo.com/bobbyiliev/how-to-install-laravel-on-digitalocean-with-1-click)

Or you could use this awesome script to do the installation:

* [LaraSail](https://devdojo.com/episode/laravel-on-digital-ocean-with-larasail)

## Rollback the Last Database Migration

Let's say that you've run a database migration but then realized that you should not have done so. Laravel makes it easy to revert/rollback your last migration. To do so, you could just run the following command:

```
php artisan migrate:rollback --step=1
```

In case that you need to revert multiple migrations, you could change the `--step=1` with the number of migrations that you want to rollback.

If you don't specify the `--step=` flag, and just run the following:

```
php artisan migrate:rollback
```

This would rollback your last batch of migrations. So let's say that you've added 5 migration files and run `php artisan migrate` to run all 5 migrations at once. This would be considered as 1 batch.

## Rollback Specific Migration

In other cases, you might want to rollback just a specific migrations file rather than the last one. You can do that with the `--path` flag followed by the path to the migrations file.

Example:

```
php artisan migrate:rollback --path=/database/migrations/the_specific_migration_file.php
```

This could be particularly handy if you want to make a minor change in your local dev environment, but you need to be careful with table drops and foreign keys.

## Rollback All Migrations

If you wanted to rollback all of your migrations, you could run the following:

```
php artisan migrate:reset
```

> Note that you should never do that in a production environment as you will lose all of your data.

The above would essentially truncate your database. In case that you wanted to drop all tables and then run the migrations from scratch, you could use the following command:

```
php artisan migrate:refresh
```

That way, you will get a fresh new database with empty tables.

## Conclusion

This is pretty much it! This is how you can rollback database migrations in Laravel!

If you are just getting started with Laravel, I would recommend going through [this Laravel introduction course](https://devdojo.com/course/laravel-7-basics).

[](https://devdojo.com/bobbyiliev/how-to-rollback-database-migrations-in-laravel)