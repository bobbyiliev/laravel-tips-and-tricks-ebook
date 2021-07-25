# How to Remove a Migration in Laravel

Adding columns or tables to your database manually could be an intimidating process and would more often than not lead to database inconsistencies between your different environments.

The Laravel migrations allow you to basically version control your database so that all members of your team could have a consistent database schema.

In this tutorial, **you will learn how to remove a migration for your Laravel application**!

Before you start, you would need to have a Laravel application up and running.

I will be using a DigitalOcean Ubuntu Droplet for this demo. If you wish, you can use my affiliate code to get [free $100 DigitalOcean credit](https://m.do.co/c/2a9bba940f39) to spin up your own servers!

If you do not have that yet, you can follow the steps from this tutorial on how to do that:

* [How to Install Laravel on DigitalOcean with 1-Click](https://devdojo.com/bobbyiliev/how-to-install-laravel-on-digitalocean-with-1-click)

Or you could use this awesome script to do the installation:

* [LaraSail](https://devdojo.com/episode/laravel-on-digital-ocean-with-larasail)

## Creating a Laravel migration

In order to create a Laravel migration, you would use the following `artisan` command:

```
php artisan make:migration create_videos_table
```

The naming convention when creating new tables is the following: 

* Start with the `create` keyword
* Followed by the name of the table, in our example this is `videos`
* Followed by the `table` keyword as we are adding a new table.

If you are adding a column to an existing table rather than a brand table, you could follow the steps in this tutorial here:

* **[How to Add a New Column to an Existing Table in a Laravel Migration](https://devdojo.com/bobbyiliev/how-to-add-a-new-column-to-an-existing-table-in-a-laravel-migration)**

Once you run the command, a new file will be created at:

```
database/migrations/the_name_of_your_migration_file.php
```

Now that we've got the migration creation covered let's see how we could actually remove a migration. 

## Remove a Migration in Laravel

We've got the `php artisan make:migration` to make migrations, but there is no command for removing them. To do so, you would need to actually delete the migrations file.

Let's cover two cases:

### Remove a migration that hasn't been executed yet

If you've only created the migration and you've not executed the `php artisan migrate` command, all you would need to do to remove the migration is to delete the file.

You could do that via your text editor or the command line with the `rm` command.

* First check if the migration has been executed yet, you could use the following command:

```
php artisan migrate:status
```

* If the migration has not been ran yet, remove the file:

```
database/migrations/the_name_of_your_migration_file.php
```

### Removing a migration that has already been executed

In case that you've ran the migration already, in order to revert it, you could use the following command:

```
php artisan migrate:rollback --step=1
```

This will revert only the last migration. After that, you could again use the `rm` command as described in the past video to actually remove the migrations file.

### Reverting all migrations (DEV environments only)

Alternatively, if you are on a local dev environment and you don't actually need the data in the database, you could run `migrate:fresh` to actually revert all migrations and then run them again.

> Note: **if you run migrate fresh, this will wipe all of your data, so you need to be careful with that!**

## Conclusion

If you are just getting started with Laravel, make sure to check out this introduction course here:

[Getting started with Laravel](https://devdojo.com/course/laravel-7-basics)

If you want to learn more about SQL in general, make sure to check out this [free introduction to SQL eBook here](https://github.com/bobbyiliev/introduction-to-sql).

[Originally posted here](https://devdojo.com/bobbyiliev/how-to-remove-a-migration-in-laravel)