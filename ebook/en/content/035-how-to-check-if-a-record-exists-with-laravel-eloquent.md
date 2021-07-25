# How to check if a record exists with Laravel Eloquent

The Eloquent ORM included with Laravel provides you with an easy way of interacting with your database. This simplifies all CRUD (Create, read, update, and delete) operations and any other database queries.

In this tutorial, you will learn how to check if a record exists with Laravel Eloquent!

Before you start, you would need to have a Laravel application up and running.

I will be using a DigitalOcean Ubuntu Droplet for this demo. If you wish, you can use my affiliate code to get [free $100 DigitalOcean credit](https://m.do.co/c/2a9bba940f39) to spin up your own servers!

If you do not have that yet, you can follow the steps from this tutorial on how to do that:

* [How to Install Laravel on DigitalOcean with 1-Click](https://devdojo.com/bobbyiliev/how-to-install-laravel-on-digitalocean-with-1-click)

Or you could use this awesome script to do the installation:

* [LaraSail](https://devdojo.com/episode/laravel-on-digital-ocean-with-larasail)

## Check if a record exists

Laravel provides a really nice method called `exists`, which allows you to check if your query returns any records rather than using the  `count` method.

```
if (Post::where('slug', $slug)->exists()) {
   // post with the same slug already exists
}
```

I always prefer to use the `exists` method, but here is an alternative example using `count`:

```
if (Post::where('slug', $slug)->count() > 0) {
   // post with the same slug already exists
}
```

What we are doing here is to select all posts where the `slug` equals the slug that we've passed as an input and then do a count on that, and if it is greater than `0`, it means that a post with that slug already exists.

## Create record if it does not exist already

Laravel provides another beneficial method called `firstOrCreate`. This allows you to quickly check if a specific entry already exists and, if not, create an entry for it with 1 query.

Let's have the following example, we have a post create form where we want to check if a post with a specific slug exists, and if it does not, then we want to create the post.

By using `firstOrCreate` this will look like this:

```
    $post = Post::firstOrCreate(
        [
            'slug'             => $post->slug,
        ],
        [
            'title'            => $post->title,
            'body'             => $post->body,
            'slug'             => $post->slug,
        ]
    );
```

Here first we check if a post with that slug exists by using the following statement:

```
        [
            'slug'             => $post->slug,
        ],
```

And then if it does not exist, we create it straight away with the following values:

```
        [
            'title'            => $post->title,
            'body'             => $post->body,
            'slug'             => $post->slug,
        ]
```

## Conclusion

For more information and useful tips on Laravel Eloquent, make sure to check this tutorial here:

[Laravel Eloquent Make](https://devdojo.com/tnylea/laravel-eloquent-make)

I strongly suggest checking out the official Laravel Documentation:

* [Laravel Eloquent](https://laravel.com/docs/8.x/eloquent)

* [Laravel Database queries](https://laravel.com/docs/8.x/queries)

[Originally posted here](https://devdojo.com/bobbyiliev/how-to-check-if-a-record-exists-with-laravel-eloquent)