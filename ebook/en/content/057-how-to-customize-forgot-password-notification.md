# How to customize forgot password notification

There are some cases where the default forgot password email template does not fit for your project,
in these cases you can create a new custom notification and override how the `User` model would use it. 

## Create a custom notification

```
php artisan make:notification CustomResetPasswordNotification
```

You can make easier your development by extends from the default Notification class:

```php
class ResetPasswordNotification extends Notification
{
    // custom code
}
}
```

## Override the notification

```php
class User 
{
    public function sendPasswordResetNotification($token)
    {
        $this->notify(new CustomResetPasswordNotification($token));
    }
}
```

## Conclusion

This was just a quick example of **how to customize forgot password notification.**.

Of course as anything in Laravel there are a lot of ways to make this changes, but here is a very simple approach to use a custom notification.

If you are new to Laravel, I would recommend checking out this [Introduction to Laravel 7](https://www.youtube.com/watch?v=ZYDBQcnkj38&list=PL_UnIDIwT95Mn-Txakyt5x183aVXdve2R) free course by **DevDojo**.
