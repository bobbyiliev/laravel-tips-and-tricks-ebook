# How to get the current date and time in Laravel

Working with date and time could be pretty challenging. Luckily we have the `Carbon` package that makes this super easy!

Carbon is a simple PHP API extension for DateTime. You can find more information about Carbon on their official website [here](https://carbon.nesbot.com).

Laravel also provides a lot of handy methods that you could use throughout your application.

In this tutorial, **you will learn how to get the current date and time in Laravel**!

Before you start, you would need to have a Laravel application up and running.

I will be using a DigitalOcean Ubuntu Droplet for this demo. If you wish, you can use my affiliate code to get [free $100 DigitalOcean credit](https://m.do.co/c/2a9bba940f39) to spin up your own servers!

If you do not have that yet, you can follow the steps from this tutorial on how to do that:

* [How to Install Laravel on DigitalOcean with 1-Click](https://devdojo.com/bobbyiliev/how-to-install-laravel-on-digitalocean-with-1-click)

Or you could use this awesome script to do the installation:

* [LaraSail](https://devdojo.com/episode/laravel-on-digital-ocean-with-larasail)

## Using Carbon to get the current date and time

As of the time being, `Carbon` comes included out of the box with all new Laravel applications.

In order to include `Carbon` to a specific controller, for example, is to include this line:

```
<?php
use Carbon\Carbon;
``` 

Then you will be able to use all of the handy methods that `Carbon` provides.

The main method that we will cover is the `now()` method, and in order to use it you could do the following:

```
<?php
use Carbon\Carbon;

$currentTime = Carbon::now();
```

Now, if you were to use `dd($currentTime)`, you would get the following output:

```
Carbon @1624629716 {#849 ▼
  date: 2021-06-25 14:01:56.305923 UTC (+00:00)
}
```

To get this to a more human-readable format, you could use the `toDateTimeString()` method:

```
<?php
use Carbon\Carbon;

$currentTime = Carbon::now();

echo $currentTime->toDateTimeString();
```

Output:

```
"2021-06-25 14:04:25"
```

Or alternatively, you could convert this to an array:

```
$currentTime->toArray();
```

If you used `dd($currentTime->toArray());` you would get the following output:

```
array:12 [▼
  "year" => 2021
  "month" => 6
  "day" => 25
  "dayOfWeek" => 5
  "dayOfYear" => 176
  "hour" => 14
  "minute" => 14
  "second" => 58
  "micro" => 12380
  "timestamp" => 1624630498
  "formatted" => "2021-06-25 14:14:58"
  "timezone" => CarbonTimeZone {#853 ▼
    timezone: UTC (+00:00)
    +"timezone_type": 3
    +"timezone": "UTC"
  }
]
```

In some cases, you might want to output the current date directly in your Blade template. Let's see how to easily do that!

## Using the `now()` helper function

Laravel provides a nice helper function called `now()`, which creates a new `Carbon` instance.

You can call the `now()` helper function directly in your Blade view as follows:

```
<p>{{  now()->toDateTimeString() }}</p>
```

The output would be again as follows:

```
"2021-06-25 14:06:16"
```

If you wanted to get the time for a specific timezone, you could pass the timezone as a parameter to the `now` helper function:

```
now("Europe/Paris");
```

## Conclusion

If you are just getting started with Laravel, make sure to check out this introduction course here:

[Getting started with Laravel](https://devdojo.com/course/laravel-7-basics)

If you want to learn more about PHP in general, make sure to check out this [free PHP basics course here](https://devdojo.com/course/php-basics).

[Originally posted here](https://devdojo.com/bobbyiliev/how-to-get-the-current-date-and-time-in-laravel)**