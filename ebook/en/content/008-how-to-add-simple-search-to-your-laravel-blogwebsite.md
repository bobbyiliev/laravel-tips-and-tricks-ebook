# How to add simple search to your Laravel blog/website

There are many ways of adding search functionality to your Laravel website. 

For example, you could use [Laravel Scout](https://laravel.com/docs/7.x/scout) which is an official Laravel package, you can take a look at this tutorial here on [how to install, setup and use Laravel scout with Algolia](https://devdojo.com/devdojo/laravel-scout).

However, in this tutorial here, we will focus on building a very simple search method without the need of installing additional packages.

Before you begin you need to have Laravel installed. 

If you do not have that yet, you can follow the steps on how to do that [here](https://devdojo.com/bobbyiliev/laravel-app-on-digital-ocean-ubuntu-1904-droplet-step-by-step-guide) or watch this video tutorial on [how to deploy your server and install Laravel from scratch](https://www.youtube.com/watch?v=RrhpbFCOlZ0&list=PLY7SzAmnEqp6bOl-AehM9dX3UKlxTjMVD).

You would also need to have a model ready that you would like to use. For example, I have a small blog with a `posts` table and `Post` model that I would be using.

## Controller changes

First, create a controller if you do not have one already. In my case, I will name the controller `PostsController` as it would be responsible for handling my blog posts. 

To create that controller just run the following command:

```
php artisan make:controller PostsController
```

Then open your controller with your text editor, and add the following `search` method:

```
public function search(Request $request){
    // Get the search value from the request
    $search = $request->input('search');

    // Search in the title and body columns from the posts table
    $posts = Post::query()
        ->where('title', 'LIKE', "%{$search}%")
        ->orWhere('body', 'LIKE', "%{$search}%")
        ->get();

    // Return the search view with the resluts compacted
    return view('search', compact('posts'));
}
```

Note that you would need to change the table names which you would like to search in.

In the example above we are searching in the title and body columns from the posts table.

## Route changes

Once our controller is ready, we need to add a new route in the `web.php` file:

```
Route::get('/search/', 'PostsController@search')->name('search');
```

We will just use a standard get request and map it to our `search` method in the `PostsController`.

## Blade view changes

Now that we have the route and the controller all sorted out, we just need to add a form in our `search.blade.php` file.

I will use the following simple `GET` form:

```
<form action="{{ route('search') }}" method="GET">
    <input type="text" name="search" required/>
    <button type="submit">Search</button>
</form>
```

Feel free to add this to your existing view and style it accordingly with your classes.

Then to display the results, what you could do is use the following `forearch` loop in your view:

```
@if($posts->isNotEmpty())
    @foreach ($posts as $post)
        <div class="post-list">
            <p>{{ $post->title }}</p>
            <img src="{{ $post->image }}">
        </div>
    @endforeach
@else 
    <div>
        <h2>No posts found</h2>
    </div>
@endif
```

The above would display your posts if there are any found and would print `No posts found` message if there are none.

## Conclusion

This is just one way of building a simple search Laravel! 

If you are just getting started with Laravel I would recommend going through [this Laravel introduction course](https://devdojo.com/course/laravel-7-basics).

[Originally posted here](https://devdojo.com/bobbyiliev/how-to-add-simple-search-to-your-laravel-blogwebsite)