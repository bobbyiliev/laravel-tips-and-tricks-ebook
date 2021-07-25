# How to Add a New Column to an Existing Table in a Laravel Migration

The Laravel Migrations allow you to manage your database structure by creating new tables and columns. The Laravel migrations are like version control for your database.

In this tutorial, **you will learn how to add a new column to an existing table in a Laravel Migration**!

Before you start, you would need to have a Laravel application up and running.

I will be using a DigitalOcean Ubuntu Droplet for this demo. If you wish, you can use my affiliate code to [get free $100 DigitalOcean credit](https://m.do.co/c/2a9bba940f39) to spin up your own servers!

If you do not have that yet, you can follow the steps from this tutorial on how to do that:

* [How to Install Laravel on DigitalOcean with 1-Click](https://devdojo.com/bobbyiliev/how-to-install-laravel-on-digitalocean-with-1-click)

Or you could use this awesome script to do the installation:

* [LaraSail](https://devdojo.com/episode/laravel-on-digital-ocean-with-larasail)

# Creating a new table with a migration

Let's first start by creating a new table called `tasks`.

In order to create a new table, you could use the following `artisan` command:

```
php artisan make:migration create_tasks_table
```

Output:

```
Created Migration: 2020_12_23_133641_create_tasks_table
```

This would generate a new migration file for you at:

```
database/migrations/2020_12_23_133641_create_tasks_table.php
```

The content of the file would look like this:

```
<?php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

class CreateTasksTable extends Migration
{
    /**
     * Run the migrations.
     *
     * @return void
     */
    public function up()
    {
        Schema::create('tasks', function (Blueprint $table) {
            $table->bigIncrements('id');
            $table->timestamps();
        });
    }

    /**
     * Reverse the migrations.
     *
     * @return void
     */
    public function down()
    {
        Schema::dropIfExists('tasks');
    }
}
```

The Laravel migrations will use the `Schema` facade to create and modify database tables and columns:

```
        Schema::create('tasks', function (Blueprint $table) {
            $table->bigIncrements('id');
            $table->timestamps();
        });
```

Inside the facade, you could specify the different columns that you want to add.

So let's go ahead and add a new column called `title` which would hold the title of our tasks:

```
        Schema::create('tasks', function (Blueprint $table) {
            $table->bigIncrements('id');
            $table->string('title');
            $table->timestamps();
        });
```

After that, to run the migration, use this `artisan` command here:

```
php artisan migrate
```

Output:

```
Migrating: 2020_12_23_133641_create_tasks_table
Migrated:  2020_12_23_133641_create_tasks_table (0.02 seconds)
```

Next, let's look into how to add a new column to that existing table without modifying the old migration file.

# Add a New Column to an Existing Table

Now, let's say that we wanted to add a `description` column to our existing `tasks` table where we would keep the description of the tasks that we have.

To do we can again use the `php artisan make:migration` command, but this time we can specify the table that we want to add the column to with the `--table` argument:

```
php artisan make:migration add_description_to_tasks --table="tasks"
```

Output:

```
Created Migration: 2020_12_23_134156_add_description_to_tasks
```

> It is considered a good practice to use a descriptive name for your migration.

This will again generate a new file at:

```
database/migrations/2020_12_23_134156_add_description_to_tasks.php
```

> Note: The timestamp at the beginning of the file will indicate when the file was created

The content of the file will look like this:

```
<?php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

class AddDescriptionToTasks extends Migration
{
    /**
     * Run the migrations.
     *
     * @return void
     */
    public function up()
    {
        Schema::table('tasks', function (Blueprint $table) {
            //
        });
    }

    /**
     * Reverse the migrations.
     *
     * @return void
     */
    public function down()
    {
        Schema::table('tasks', function (Blueprint $table) {
            //
        });
    }
}
```

To add the new column, just specify it again in the `up()` method:

```
public function up()
{
    Schema::table('tasks', function($table) {
        $table->text('description');
    });
}
```

Another important thing to keep in mind here is that you need to update the `down()` method as well and add a `dropColumn()` method indicating that in case someone runs a migration refresh, the column should be dropped:

```
public function down()
{
    Schema::table('tasks', function($table) {
        $table->dropColumn('description');
    });
}
```

Finally, save the file and rerun your migrations:

```
php artisan migrate
```

Output:

```
Migrating: 2020_12_23_134156_add_description_to_tasks
Migrated:  2020_12_23_134156_add_description_to_tasks (0.03 seconds)
```

And this is pretty much it! This is how you can add a new column to an existing table!

# Conclusion

If you are just getting started with Laravel, make sure to check out this [introduction to Laravel course here](https://devdojo.com/course/laravel-7-basics).

I also strongly suggest checking out the official Laravel Documentation:

* [Laravel Documentation](https://laravel.com/docs/8.x/)

[Originally posted here](https://devdojo.com/bobbyiliev/how-to-add-a-new-column-to-an-existing-table-in-a-laravel-migration)