# How to Add Multiple Where Clauses Using Laravel Eloquent

The Eloquent ORM included with Laravel provides you with an easy way of interacting with your database. This simplifies all CRUD (Create, read, update, and delete) operations and any other database queries.

In this tutorial, **you will learn how to add multiple where clauses using Laravel Eloquent**!

Before you start, you would need to have a Laravel application up and running.

I will be using a DigitalOcean Ubuntu Droplet for this demo. If you wish, you can use my affiliate code to [get free $100 DigitalOcean credit](https://m.do.co/c/2a9bba940f39) to spin up your own servers!

If you do not have that yet, you can follow the steps from this tutorial on how to do that:

* [How to Install Laravel on DigitalOcean with 1-Click](https://devdojo.com/bobbyiliev/how-to-install-laravel-on-digitalocean-with-1-click)

Or you could use this awesome script to do the installation:

* [LaraSail](https://devdojo.com/episode/laravel-on-digital-ocean-with-larasail)

## Chaining multiple where clauses together 

Generally speaking, you could chain multiple `where` methods together like this:

```
        $posts = Post::where('status', 'published')
                        ->where('featured', '')
                        ->where('author_id', 1)
                        ->toSql();
        dd($posts);
```

The output of the above to pure SQL with the `toSql` method would look like this:

```
"select * from `posts` where `status` = ? and `featured` = ? and `author_id` = ?"
```

So the first `where` method is translated to an actual `where` in SQL, and then each `where` clause is translated to an `AND` in SQL.

## Passning an array to the `where` method

An alternative to the above would be to pass an array with your specific rules. This would look like this:

```
        $posts = Post::where(['status' => 'published',
                            'featured' => '',
                            'author_id' => 1,
                            ])
                        ->toSql();
        dd($posts);
```

Output:

```
"select * from `posts` where (`status` = ? and `featured` = ? and `author_id` = ?)"
```

In case that you needed to give different rules rather than the default `equals` to, you could use the following syntax:

```
$posts = Post::where([
                    ['status', '=', 'published'],
                    ['featured', '!=', 'no'],
                    ['author_id', '>', 0],
                    ])
                ->toSql();
dd($posts);
```

The raw SQL for the above would look like this:

```
"select * from `posts` where (`status` = ? and `featured` != ? and `author_id` > ?)"
```

## Using `orWhere` Clauses

In case you want your clauses to be joined with `OR` rather than `AND`, you could use the `orWhere` method:

```
$posts = Post::where('status', 'published')
                ->orWhere('featured', '')
                ->orWhere('author_id', 1)
                ->toSql();
dd($posts);
```

Output:

```
"select * from `posts` where `status` = ? or `featured` = ? or `author_id` = ?"
```

## Conclusion

For more information and useful tips on Laravel Eloquent, make sure to check this tutorial here:

* [Laravel Eloquent Make](https://devdojo.com/tnylea/laravel-eloquent-make)

I strongly suggest checking out the official Laravel Documentation:

* [Laravel Eloquent](https://laravel.com/docs/8.x/eloquent)

[Originally posted here](https://devdojo.com/bobbyiliev/how-to-add-multiple-where-clauses-using-laravel-eloquent)