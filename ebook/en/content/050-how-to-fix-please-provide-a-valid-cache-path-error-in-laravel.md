# How to fix 'Please provide a valid cache path' error in Laravel

The other day, I was setting up a local development environment for an existing project when I encountered the **'Please provide a valid cache path'** error.

As the error itself is not very descriptive and could leave you thinking that something is wrong with your configuration, I've decided to write a short post on how to get this sorted out!

## Creating the cache folders

By default Laravel stores its temporary files at the `storage/framework` directory. In there there should be 3 more folders: `sessions`, `views` and `cache`. 

That is where Laravel will store its generated blade views, cache and sessions.

Without those 3 directories you might see the error above.

To create the directories you could run the following command.

* First use the `cd` command to access the location of your Laravel application and then run:

```
mkdir storage/framework/{sessions,views,cache}
```

The above command will create the 3 directories in question.

## Clearing the cache

After that you could run the following commands to clear your cache and make sure that it works as expected:

```
php artisan cache:clear
php artisan config:clear
php artisan view:clear
```

You should see the following output:

```
Application cache cleared!
Configuration cache cleared!
Compiled views cleared!
```

## Conclusion

This is pretty much it! I hope that this post helps you to solve the problem in question!

[Originally posted here](https://devdojo.com/bobbyiliev/how-to-fix-please-provide-a-valid-cache-path-error-in-laravel)