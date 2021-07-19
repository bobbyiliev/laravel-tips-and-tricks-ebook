# How to Quickly Change the Password for a User in Laravel

In some cases, you might want to reset the password for your Laravel user quickly. Another reason might be that you could be having problems with your emails, and the reset password email is not being delivered.

However, unlike WordPress, for example, where you could simply use `MD5` to encrypt your password and update it in your `users` table, Laravel uses hashing for the password encryption, so you can not change the password directly in your database.

Here are a couple of quick ways that you could use to reset your user password quickly!

Before you begin, you need to have Laravel installed.

If you do not have that yet, you can follow the steps on how to do that [here](https://devdojo.com/bobbyiliev/laravel-app-on-digital-ocean-ubuntu-1904-droplet-step-by-step-guide) or watch this video tutorial on [how to deploy your server and install Laravel from scratch](https://www.youtube.com/watch?v=RrhpbFCOlZ0&list=PLY7SzAmnEqp6bOl-AehM9dX3UKlxTjMVD).

You would also need to have a model ready that you would like to use. For example, I have a small blog with a `posts` table and `Post` model that I would be using.

## Reset password with `tinker`

If you have been working with Laravel for a while, you've most probably used `thinker` to do some testing directly from your terminal.

To get started, run the following command:

```
php artisan tinker
```

Depending on the PHP version that you are using, you will see the following output:

```
Psy Shell v0.9.9 (PHP 7.4.14 — cli) by Justin Hileman
>>>
```

After that, you can write a standard query to get the user that you want to change the password for. For example, if you know the email of the user, you could do something like this:

```
$user = App\Models\User::where('email', 'your_email@example.com')->first();
```

> Note: if you are using Laravel 7 or bellow, you might have to change `App\Models\User` to `App\User`, depending on where you store your models at.

Once you run the above, you will get the following output with some information for your user:

```
=> App\User {#3365
     id: 8,
     role_id: 1,
     name: "Bobby",
     email: "bobby@bobbyiliev.com",
     avatar: "users/default.png",
     settings: "{"locale":"en"}",
     created_at: "2021-01-29 08:21:25",
     updated_at: "2021-02-01 11:52:08",
   }
```

With that, we've got our user defined as `$user` object so we can now change the password property with:

```
$user->password = Hash::make('your_super_strong_password_here');
```

> Note: Change `your_super_strong_password_here` with the new password that you want to use.

As soon as you run this, you will get an output of your hashed password.

Then finally, to persist the changes run:

```
$user->save();
```

Output:

```
=> true
```

If you are not a fan of the terminal, you could also do the same thing, but via a controller, or for the sake of simplicity, you could add a closure in your routes file with more or less the same code as above. Let's see how to do this next!

## Reset password via a route

To do that, open the `routes/web.php` file with your favirute text editor and add the following right after the opening PHP tag:

```
<?php
Route::get('temporary-password-reset', function() {
    $user = App\Moleds\User::where('email', 'your_email@example.com')->first();
    $user->password = Hash::make('your_super_secure_password');
    $user->save();
 
    return 'Success!';
});
```

> Note: if you are using Laravel 7 or bellow, you might have to change `App\Models\User` to `App\User`, depending on where you store your models at.

Save that, and then visit the link `/temporary-password-reset` URL via your browser. This will trigger the password change. 

> Note: Make sure to delete the route, once you've changed your password!

## Conclusion

Those are 2 ways that you could use to quickly reset the password for your Laravel user!

If you are just getting started with Laravel, I would recommend going through [this Laravel introduction course](https://devdojo.com/course/laravel-7-basics).

[Originally posted here](https://devdojo.com/bobbyiliev/how-to-quickly-change-the-password-for-a-user-in-laravel)