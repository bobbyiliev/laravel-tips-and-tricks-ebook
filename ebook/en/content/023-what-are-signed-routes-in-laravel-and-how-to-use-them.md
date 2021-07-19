# What are signed routes in Laravel and how to use them

Signed routes allow you to create routes accessible only when a signature is passed as a GET parameter. This could be used for sharing a preview of a draft article or any other route that you want to be public but only accessible by people who have the signature.

You could also use signed routes to allow them access to a specific route for a set period of time. For example, if you are launching a new course or SaaS, you might want to open the registration only for a day and allow just a small number of people to sign up for your product initially.

In this tutorial, you will learn how to create signed routes for your Laravel application!

Before you start, you would need to have a Laravel application up and running.

I will be using a DigitalOcean Ubuntu Droplet for this demo. If you wish, you can use my affiliate code to get [free $100 DigitalOcean credit](https://m.do.co/c/2a9bba940f39) to spin up your own servers!

If you do not have that yet, you can follow the steps from this tutorial on how to do that:

* [How to Install Laravel on DigitalOcean with 1-Click](https://devdojo.com/bobbyiliev/how-to-install-laravel-on-digitalocean-with-1-click)

Or you could use this awesome script to do the installation:

* [LaraSail](https://devdojo.com/episode/laravel-on-digital-ocean-with-larasail)

## Defining a signed route

To keep things simple, as an example, we will create a route that returns a discount code. The route would only be available for 10 minutes so that only the first people who get to the route would get the discount code.

To create a signed route, open your `routes/web.php` file with your favorite text editor and add the following:

```
Route::get('/discount', function(){
    return 'some_discount_code_here';
})->name('discountCode')->middleware('signed');
```

A quick rundown of the route:

* First, we define a get route accessible at the `/discount` URL.
* Then we create a closure that only returns a string here. In a real-life scenario, you would use a controller and possibly a Model which returns a discount code stored in your database.
* Then we specify that this is a named route with the `name()` method.
* Finally, with the `middleware('signed')` method, we specify that this is a signed route.

Now thanks to the signed middleware, the route would only be accessible if the user has the signature hash specified as a parameter.

If you try to visit the `/discount` route directly without passing the signature, you will get a `403 Invalid signature error.

Next, we will learn how to get the temporary signed route URL!

## Generating the signature

We can use the `URL::temporarySignedRoute` method to generate the signature.

Let's quickly create a Laravel controller that will generate the signed route for us:

```
php artisan make:controller DiscountController
```

This will generate the new controller at:

```
app/Http/Controllers/DiscountController.php
```

Open the file with your favorite text editor and first include the `URL` facade:

```
use Illuminate\Support\Facades\URL;
```

After that, create a public method with the following content:

```
public function discount()
{
    return URL::temporarySignedRoute(
        'discountCode', now()->addMinutes(30)
    );
}
```

Now let's create a route that will hit this method and return the signed route! 

## Using the signed route

We will start by adding a new route, to do so open the `routes/web.php` file and add the following:

```
use App\Http\Controllers\DiscountController;

Route::get('/generate-signature', [DiscountController::class, 'discount']);
```

Now if you access the `/generate-signature` URL via your browser you will get a similar output:

```
http://example.com/discount?expires=1617628939&signature=20a44d614b6e4448c1f3a5bf78d3a44ca9b64b2afa940757bdb66ca2b1537974
```

Quick rundown:

* First, we define a public method called `discount`.
* After that, we use the `temporarySignedRoute` static method provided by the `URL` facade, and we give the following parameters:
    * `discountCode` is the name of our route
    * `now()->addMinutes(30)` this specifies that the signature will be valid for the next 30 minutes only

Now, if you visit the URL with the signature, you will get your discount code as the response.

> Note, if you get an error that the `signed` class does not exist, make sure to add the following to the `protected $routeMiddleware` array in the `app/Http/Kernel.php` file:

```
        'signed' => \Illuminate\Routing\Middleware\ValidateSignature::class,
```

The above URL will only be valid for 30 minutes, but you could generate signed URLs that are valid forever if you decided to do so.

## Conclusion

Now you know how to create signed routes in your Laravel application! There is a wide variety of scenarios when you might want to use this!

For more information on Laravel Signed Routes, make sure to check out the official docs here:

[Signed URLs](https://laravel.com/docs/8.x/urls#signed-urls)

If you are just getting started with Laravel, make sure to check out this introduction course here:

[Getting started with Laravel](https://devdojo.com/course/laravel-7-basics)

[Originally posted here](https://devdojo.com/bobbyiliev/what-are-signed-routes-in-laravel-and-how-to-use-them)