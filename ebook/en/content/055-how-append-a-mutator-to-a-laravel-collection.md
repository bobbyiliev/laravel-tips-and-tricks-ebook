# How to append a mutator to a collection

Mutators in Laravel provide us an easy way to transform a model property.

In this example a `Post` model implement a mutator based on `created_at` timestamps.

```php
class Post
{
    protected $casts = [
        'created_at' => 'date',
    ];
    
    public function getPublishedAttribute()
    {
        return $this->created_at->diffForHumans();
    }
}
```

## Append a mutator on a single model

Eloquent provides a method to append a mutator to a single model so you can return a single model with a mutator as it is another model property:

```php
public function show(Post $post)
{
    return view('post.show', ['post' => $post->append('published_at')]);
}
```

## Usage

```php
$post->published_at;
```

## Append a mutator to a collection

Ok, so right now we are able to append a mutator to a single model, if you want to append a mutator to a whole collection,
you could be tempted to add the mutator to your model `append` property.

But, most of the time it is unnecessary and even a not performant action 
to append the mutator and of course calculate it, on every instance of a model or a collection.

Another action that could be potentially a bad practice would be to return only you eloquent collection and force a blade template to append every mutator on the fly, this would lead to an N + 1 problem and should be avoided as much as possible.

So instead of append the mutator all the time you can use the collection high order proxy to append the mutator for all items in the collection:

```php
public function index()
{
    $posts = Post::query()->get();
    $posts->append('published_at');
    return view('posts.index', ['posts' => $posts]);
}
```

Now in your view you can iterate over your eloquent collection and get the mutator as it is another model property without n+1 problems and only append the mutator on this specific controller method.

```php
@foreach($user as $users)
    <p>{{ $user->published_at }}</p>
@endforeach
```

## Conclusion

This was just a quick example of **how to append a mutator to a laravel collection** and what could lead to a bad practice and n+1 query problems adn how to avoid it.

If you are new to Laravel, I would recommend checking out this [Introduction to Laravel 7](https://www.youtube.com/watch?v=ZYDBQcnkj38&list=PL_UnIDIwT95Mn-Txakyt5x183aVXdve2R) free course by **DevDojo**.
