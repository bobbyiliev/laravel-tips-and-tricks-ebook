# How to copy or move records from one table to another in Laravel

In some cases when a particular table grows too much it might slow down your Laravel website. You might want to clear old records or archive them to another table so that you could keep your main table as light as possible.

As of the time of writing this post, Laravel does not provide a helper method to move records from one table to another, so here is how you could achieve that!

As an example, I have a `posts` table and Model, and I would show you how to copy or move all posts that have not been updated in the past 5 years to another table called `legacy_posts`.

Before you begin you need to have Laravel installed.

If you do not have that yet, you can follow the steps on how to do that [here](https://devdojo.com/bobbyiliev/laravel-app-on-digital-ocean-ubuntu-1904-droplet-step-by-step-guide) or watch this [video tutorial on how to deploy your server and install Laravel from scratch](https://www.youtube.com/watch?v=RrhpbFCOlZ0&list=PLY7SzAmnEqp6bOl-AehM9dX3UKlxTjMVD).

You would also need to have a model ready that you would like to use. For example, I have a small blog with a posts table and Post model that I would be using.

## Copy all records from one table to another

The `replicate()` method provides an optimized way of creating a clone of an entire instance of a Model.

For this example, I will use my Posts model and copy all posts that have not been updated in the past 5 years to a new table called `legacy_posts`:

```
  Posts::query()
   ->where('updated_at','<', now()->subYears(5))
   ->each(function ($oldPost) {
    $newPost = $oldPost->replicate();
    $newPost->setTable('legacy_posts');
    $newPost->save();

  });
```

A quick rundown of the query:

* First we select all entries from the posts table which have not been updated in the past 5 years using the `where('updated_at','<', now()->subYears(5))` statement

* Then we create a new instance with the `replicate()` method. This would hold the result of the above query

* After that by using the `setTable('legacy_posts')` we specify the new table where we would like to store the results in 

* At the end you can see that we use the `save()` method to store all entries in the new `legacy_posts` table.

> Note: you need to have the `legacy_posts` table already created in order to use the above, otherwise you would get an error that the table does not exist.

## Move all records from one table to another

Let's say that you wanted to not only replicate the records but also remove the old records from your main posts table as well.

In this case you could use the following query:

```
  Posts::query()
  ->where('updated_at','<', now()->subYears(5))
  ->each(function ($oldRecord) {
    $newPost = $oldRecord->replicate();
    $newPost ->setTable('legacy_posts');
    $newPost ->save();

    $oldPost->delete();
  });
```

This will delete all entries from posts table which have not been updated in the past 5 years and copy them to a new table called `legacy_posts`.

## Conclusion

For more information, I would recommend going through the [official Laravel documentation regarding Replicating Models](https://laravel.com/docs/7.x/eloquent#replicating-models).

[Originally posted here](https://devdojo.com/bobbyiliev/how-to-copy-or-move-records-from-one-table-to-another-in-laravel)