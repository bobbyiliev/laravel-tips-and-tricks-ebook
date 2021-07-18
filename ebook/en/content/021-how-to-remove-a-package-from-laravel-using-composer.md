# How to remove a package from Laravel using composer

Every PHP developer should be familiar with how to use frameworks. Frameworks help make the process of development easier by simplifying common practices used in developing major web projects such as packages, modules, plug-ins, and even components.

Adding a package or packages is the primary way of adding functionality to Laravel. They might be anything from a great way to work with dates like Carbon, an entire BDD testing framework like Behat, or a package that helps users add a developer toolbar to their application that is mainly used for debugging purposes like Debugbar.

If you don't already have a Laravel application up and running, then I suggest using DigitialOceans Ubuntu Droplet. I will be using it for this demo. If you wish, you can use my affiliate code to get [free $100 DigitalOcean credit](https://m.do.co/c/2a9bba940f39) to spin up your own servers!

If you do not have that yet, you can follow the steps from this tutorial on how to do that:

* [How to Install Laravel on DigitalOcean with 1-Click](https://devdojo.com/bobbyiliev/how-to-install-laravel-on-digitalocean-with-1-click)

Or you could use this awesome script to do the installation:

* [LaraSail](https://devdojo.com/episode/laravel-on-digital-ocean-with-larasail)

## Adding a package to Laravel

Let's first add an example package to our Laravel website, which we will later use as an example package to remove.

We are going to use the Laravel Sitemap package. To install the package, just use the following composer command:

```
composer require spatie/laravel-sitemap
```

This will automatically add the following entry in your `composer.json` file:

```
"spatie/laravel-sitemap": "^5.8"
```

And will download the package files in the `vendor/spatie/laravel-sitemap` folder.

Now that we have added a package, we can use it as an example and remove it.

## Removing a package from Laravel using composer

To remove a Laravel package, we just need to run a single command:

```
composer remove spatie/laravel-sitemap
```

> **Change the `spatie/laravel-sitemap` with the name of the package that you want to remove.**

This will remove the line from your `compser.json` file and also the files from the `vendor` folder.

Don't forget that you have to edit your code and ensure that the package is not being used.

## Conclusion

Composer makes it super easy to add and remove Laravel packages from your projects.

Make sure to star the project on GitHub:

* [Composer GitHub](https://github.com/composer/composer)

If you want to learn more about Laravel packages, then I suggest you check out this [Create a Laravel Package](https://devdojo.com/course/create-a-laravel-package) course.

[Originally posted here](https://devdojo.com/bobbyiliev/how-to-remove-a-package-from-laravel-using-composer)