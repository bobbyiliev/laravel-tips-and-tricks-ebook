# How to fire an event when user is logged in

Laravel provides some events by default to handle Authentication flow natively, here an example with the login event.

The EventServiceProvider allow to tight events with listeners, in this case a custom listener to an event that the framework provides.

## Create a custom service provider

```
php artisan make:listener UpdateUserLastLoginListener
```

Here you can add any logic, in this example the listener would update the new login timestamp in a `last_login_at` column in `User` model.

```php
public function handle($event)
{
    $event->user->update('last_login_at' => now());
}
```

Then we need to tight the new listener to the Login event, this event already exists and is native from the framework, so in `EventServiceProvider.php` file:

```php
protected $listen = [
    Login::class => [
        UpdateUserLastLoginListener::class,
    ],
];
```

And now everytime a user logged in this listener would be in charge to update the `last_login_at` column for you, without changing any code in the authentication code.

## Conclusion

This was just a quick example of **how to fire an event when a user is logged in.**.

This was just a simple example of how you can take an advantage of default events that already exists on the framework, 
there are more methods like, `Registered`, `Verified` and `Logout` events, where you can tight your own logic 
by using laravel listeners.

If you are new to Laravel, I would recommend checking out this [Introduction to Laravel 7](https://www.youtube.com/watch?v=ZYDBQcnkj38&list=PL_UnIDIwT95Mn-Txakyt5x183aVXdve2R) free course by **DevDojo**.
