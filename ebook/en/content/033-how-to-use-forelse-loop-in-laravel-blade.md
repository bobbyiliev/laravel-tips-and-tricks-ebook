# How to use Forelse loop in Laravel Blade

If you have ever done any coding you are most likely well familiar with the `foreach` loops. Without any doubt, a `foreach` loop is one of the best ways to iterate over the elements of the collection.

However, in case you have an empty collection, you would need an additional `if` statement so that you could point a valid message to your users.

Luckily Laravel provides awesome Blade Templates that you could use to make your life easier!

In this post, I will show you how to use `forelse` in Laravel!

Before you get started you would need to have Laravel already installed.

If this is not the case you can follow the steps here on [How to Install Laravel on DigitalOcean with 1-Click?](https://devdojo.com/bobbyiliev/how-to-install-laravel-on-digitalocean-with-1-click)!

## Check if not empty then

What I would usually do in order to check if a collection is empty in my Blade view is to use an `if-else` statement like this:

```
@if($posts->isNotEmpty())

    @foreach ($posts as $post)

        <p>This is the post title {{ $post->title}}</p>

    @endforeach

@else

    <p>No posts found</p>

@endif
```

In the above example, we first wrap up our `foreach` loop in an `if` statement, and by using the `isNotEmpty()` we check if the collection is empty, and in case that it is empty we then print the `No posts found` message.

This works pretty well, but Laravel has a more elegant way of doing things!

## Forelse example

Rather than having to nest our `foreach` loop inside of an `if` statement, what we could do instead is use the `forelse` blade template:

```
@forelse ($posts as $post)

    <p>This is the post title {{ $post->title}}</p>

@empty

    <p>No posts found</p>

@endforelse
```

As you can see we would get the same result but with less code and it is much easier to read!

## Conclusion

You now know how to use `forelse` in Blade views and have much more cleaner and easier to read code!

For more great Blade templates, I would recommend checking out the official documentation [here](https://laravel.com/docs/8.x/blade).

[Originally posted here](https://devdojo.com/bobbyiliev/how-to-use-forelse-loop-in-laravel-blade)