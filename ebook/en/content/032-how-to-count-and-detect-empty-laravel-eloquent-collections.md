# How to Count and Detect Empty Laravel Eloquent Collections

The Eloquent ORM included with Laravel provides you with an easy way of interacting with your database. This simplifies all CRUD (Create, read, update, and delete) operations and any other database queries.

Laravel provides a lot of handy methods that you could use to work with your Eloquent collections.

In this tutorial, **you will learn how count and detect empty Laravel Eloquent collections**!

Before you start, you would need to have a Laravel application up and running.

I will be using a DigitalOcean Ubuntu Droplet for this demo. If you wish, you can use my affiliate code to get [free $100 DigitalOcean credit](https://m.do.co/c/2a9bba940f39) to spin up your own servers!

If you do not have that yet, you can follow the steps from this tutorial on how to do that:

* [How to Install Laravel on DigitalOcean with 1-Click](https://devdojo.com/bobbyiliev/how-to-install-laravel-on-digitalocean-with-1-click)

Or you could use this awesome script to do the installation:

* [LaraSail](https://devdojo.com/episode/laravel-on-digital-ocean-with-larasail)

We will use a model called `Post` as an example in this tutorial.

## Check if a collection is empty

In order to check if a collection is empty, you could use the `isEmpty()` method. This would look as follows:

```
$posts= Model::where('active', true)->get();

if ($posts->isEmpty($posts)) {
    // Returns true when there are *no* posts
}
```

## Check if a collection is **not** empty

Similar to the `isEmpty()` method, there is a `isNotEmpty()` method. The syntax is the same:

```
$posts = Model::where('active', true)->get();

if ($posts->isNotEmpty($posts)) {
    // Returns true when there are posts
}
```

This could be quite handy when displaying the posts on a website for example, that way you could indicate that the user has not yet added any posts.

## Counting the records of a collection

With SQL if you wanted to get how many records match a specific query, you could use the `COUNT(*)` function, the syntax would look like this:

```
SELECT COUNT(*) FROM posts WHERE active='1';
```

In case that you had 5 active posts, the result would be 5.

When counting the total elements in a collection, the method is also called `count()`. The syntax would look like this:

```
$posts = Model::where('active', true)->get();

if ($posts->count() > 0) {
    // More than 0 posts
} else {
    / 0 posts
}
```

The `count()` method basically returns the total number of records in result.

If you wanted to check if [check a specific record is “not null” with Laravel Eloquent](https://devdojo.com/bobbyiliev/how-to-check-if-not-null-with-laravel-eloquent) make sure to check out this post here. 

## Conclusion

If you are just getting started with Laravel, make sure to check out this introduction course here:

[Getting started with Laravel](https://devdojo.com/course/laravel-7-basics)

If you want to learn more about PHP in general, make sure to check out this [free PHP basics course here](https://devdojo.com/course/php-basics).

[Originally posted here](https://devdojo.com/bobbyiliev/how-to-count-and-detect-empty-laravel-eloquent-collections)