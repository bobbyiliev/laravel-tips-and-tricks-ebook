# How to filter routes in Laravel

When your application grows the routes becomes difficult to read when you execute `php artisan route:list`

There would be nice if there is some flag to filter a route, well this is not available, 
but as it is a terminal command we can use the `grep` param to filter the output from the terminal.

* * *

Steps
-----

In the terminal:

* Inside your project directory `cd <your-project>`
* Show or hide columns
* Search by term

* * *

Filter routes by term
-------------

### 1\. Execute the command with columns flag

The output of the route list command returns a lot of useful data, but usually we only need the uri, the method and the name.

Laravel provide us with a `columns` flag to show only the columns that are necessary.

```
php artisan route:list --columns=uri,method,name
```

### 2\. Filter a route

If you are using the route names convention like resource probably your project have a route like this: `users.index`. 

If your app is serving an API it could have a route name like this: `api.users.index`.

And the app could probably have routes like: 

    * `api.users.index`
    * `api.users.show`
    * `api.users.update`
    * `api.users.store`
    * `api.users.delete`

You can filter partially or with a complete route string, in the example below it would return all the routes with the prefix `api.users`:

```
php artisan route:list --columns=uri,method,name |grep api.users
```

## Conclusion

This was just a quick example of **how to filter some group a routes between all your routes**.

If you are new to Laravel, I would recommend checking out this [Introduction to Laravel 7](https://www.youtube.com/watch?v=ZYDBQcnkj38&list=PL_UnIDIwT95Mn-Txakyt5x183aVXdve2R) free course by **DevDojo**.
