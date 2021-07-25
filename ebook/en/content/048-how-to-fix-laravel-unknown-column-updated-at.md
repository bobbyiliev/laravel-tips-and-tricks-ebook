# How to fix Laravel Unknown Column 'updated_at'

The Eloquent ORM included with Laravel provides you with an easy way of interacting with your database. This simplifies all CRUD (Create, read, update, and delete) operations and any other database queries.

As described in the official [Laravel documentation](https://laravel.com/docs/8.x/eloquent#defining-models), Eloquent expects the `created_at` and `updated_at` columns to exist on your model's corresponding database table.

However, in some specific cases you might not have those two tables in place.

In this tutorial, **you will learn how to fox the `Laravel Unknown Column 'updated_at'` error by disabling the Laravel timestamps for a specific model**!

Before you start, you would need to have a Laravel application up and running.

I will be using a DigitalOcean Ubuntu Droplet for this demo. If you wish, you can use my affiliate code to get [free $100 DigitalOcean credit](https://m.do.co/c/2a9bba940f39) to spin up your own servers!

If you do not have that yet, you can follow the steps from this tutorial on how to do that:

* [How to Install Laravel on DigitalOcean with 1-Click](https://devdojo.com/bobbyiliev/how-to-install-laravel-on-digitalocean-with-1-click)

Or you could use this awesome script to do the installation:

* [LaraSail](https://devdojo.com/episode/laravel-on-digital-ocean-with-larasail)

## Disable the timestamp columns in your Model

In order to disable the timestamp columns for a specific model, all that you would need to do is define the a public property called `$timestamps` and set this to false. 

That way, when you try to update your model, you will not get the `Unknown Column 'updated_at'` error.

Let's have a model called `Video` as an example:

```
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Model;

class Video extends Model
{
    // Disable the model timestamps
    public $timestamps = false;
}
```

With that, Eloquent will no longer be looking for the `created_at` and the `updated_at` columns.

## Change the name of the timestamp tables

In order cases, you might have the timestamp columns present, but with different names, so you would not want to disable the `timestamps` but instead specify the correct names of the tables.

To do so, all that you have to do is specify the following two constants in your Model:

```
<?php

class Video extends Model
{
    const CREATED_AT = 'creation_date';
    const UPDATED_AT = 'updated_date';
}
```

> Adjust the contestants accordingly depending on your needs

That way, Eloquent will be looking for a `updated_date` table rather than `updated_at` as default. 

## Conclusion

If you are just getting started with Laravel, make sure to check out this introduction course here:

[Getting started with Laravel](https://devdojo.com/course/laravel-7-basics)

If you want to learn more about SQL in general make sure to check out this [free introduction to SQL eBook here](https://github.com/bobbyiliev/introduction-to-sql).

[Originally posted here](https://devdojo.com/bobbyiliev/how-to-fix-laravel-unknown-column-updated-at)