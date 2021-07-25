# How to Get the Last Inserted Id Using Laravel Eloquent

The Eloquent ORM included with Laravel provides you with an easy way of interacting with your database. This simplifies all CRUD (Create, read, update, and delete) operations and any other database queries.

In this tutorial, **you will learn how to get the Last Inserted Id Using Laravel Eloquent**!

Before you start, you would need to have a Laravel application up and running.

I will be using a DigitalOcean Ubuntu Droplet for this demo. If you wish, you can use my affiliate code to [get free $100 DigitalOcean credit](https://m.do.co/c/2a9bba940f39) to spin up your own servers!

If you do not have that yet, you can follow the steps from this tutorial on how to do that:

* [How to Install Laravel on DigitalOcean with 1-Click](https://devdojo.com/bobbyiliev/how-to-install-laravel-on-digitalocean-with-1-click)

Or you could use this awesome script to do the installation:

* [LaraSail](https://devdojo.com/episode/laravel-on-digital-ocean-with-larasail)

## Last Inserted Id Using Laravel Eloquent

Let's say that we have a newsletter sign up form where people could sign up, and then after successful signup, we want to get the ID of the entry.

To achieve that, you would need to already have a Model and a controller. Here is an example method that we would use:

```
public function signUp() {

    $subscriber = new Subscriber();
    $subscriber->name = 'Bobby';
    $subscriber->name = 'hello@bobbyiliev.com';  

    $subscriber->save();
}
```

Once the new subscriber is saved, we can simply use `return $subscriber->id` to retrieve the ID.

So the complete method will look like this:

```
public function signUp() {

    $subscriber = new Subscriber();
    $subscriber->name = 'Bobby';
    $subscriber->name = 'hello@bobbyiliev.com';  

    $subscriber->save();

    return $subscriber->id;  // this will return the saved subscriber id

}
```

In case that you are building an API, you could return the response in JSON with:

```
return response()->json(array('success' => true, 'last_insert_id' => $subscriber->id), 200);
```

## Conclusion

For more information and useful tips on Laravel Eloquent, make sure to check this tutorial here:

* [Laravel Eloquent Make](https://devdojo.com/tnylea/laravel-eloquent-make)

I strongly suggest checking out the official Laravel Documentation:

* [Laravel Eloquent](https://laravel.com/docs/8.x/eloquent)

[Originally posted here](https://devdojo.com/bobbyiliev/how-to-get-the-last-inserted-id-using-laravel-eloquent)