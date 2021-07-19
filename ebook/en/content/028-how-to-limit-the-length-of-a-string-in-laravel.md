# How to limit the length of a string in Laravel

There are many different ways to limit the length of a string. For example, you could use CSS, JavaScript, or do it through PHP.

Laravel also provides a nice helper to make this easy!  We will be using the `Str` class from `Illuminate\Support\Str` namespace.

Before you begin you need to have Laravel installed. If you do not have that yet, you can follow the steps on how to do that [here](https://devdojo.com/bobbyiliev/laravel-app-on-digital-ocean-ubuntu-1904-droplet-step-by-step-guide) or watch this video tutorial on [how to deploy your server and install Laravel from scratch](https://www.youtube.com/watch?v=RrhpbFCOlZ0&list=PLY7SzAmnEqp6bOl-AehM9dX3UKlxTjMVD).

You would also need SSH access to your server.

## Limit string length in Blade

In order to limit the length of a string directly in your blade files, you can use the following:

```
<p>
    {{ Str::limit($your_string, 50) }}
</p>
```

You don't have to import the namespace as this is a global "helper" PHP function available out of the box with Laravel.

Just change the `$your_string` part with your actual string and also the `50` part with the number of characters that you would like to limit your string to.

## Limit string length in Model

You can use the same approach but directly in your Model rather than doing this in your views each time:

```
...
use Illuminate\Support\Str;

class Product
{
    const LIMIT = 50;

    protected $fillable = [
        ..., 'description'
    ]

    public function limit()
    {
        return Str::limit($this->description, YourClass::LIMIT )
    }
}
```

Then in your blade you wouldjust need to call this method:

```
<p>
    {{ $product->limit}}
</p>
```

This is a bit cleaner as you specify the length in one file and then reuse it in multiple places.

## Limit string length in Controller

You could also add the logic in your controller. So before returing your view it would look like this:

```
<?php

namespace App\Http\Controllers;

use App\Http\Controllers\Controller;
use App\Product;

class ProductController extends Controller
{
    public function show($id)
    {
        $product = User::findOrFail($id);
        $product->description = Str::limit($product->description, 50);
        return view('user.profile', compact('product'));
    }
}
```

Then in your view you would just need to do:

```
<p>
    {{ $product->description }}
</p>
```

Of course, you could use the same approach and even create a service provider or limit the length of your string before storing it in your database.

## Conclusion

Laravel makes it quite easy to limit the length of a string both in your blade view, your controller, and even in your model.

For more useful Laravel helpers, I would recommend checking out the official documentation [here](https://laravel.com/docs/7.x/helpers).

[Originally posted here](https://devdojo.com/bobbyiliev/how-to-limit-the-length-of-a-string-in-laravel)