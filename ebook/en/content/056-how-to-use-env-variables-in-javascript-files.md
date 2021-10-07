# How to use env variables in javascript

In some project we are need to add some configuration variables from `.env` file to a javascript file like `webpack.mix.js` file.

Imagine that you need use the key `APP_URL` from `.env` file, the new mix version support the same `process` syntax as VueCli and other tools.

## An example

Here an example where it configures Laravel mix to use the browserSync feature to get hot reload in our application:

### ENV file

```dotenv
APP_URL=http://localhost
```

### webpack.mix.js

Instead of hard code the string, you can use the `process` to use only one file to set all your configuration variables:

```js
if (! mix.inProduction()) {
    mix.browserSync({
        proxy: process.env.APP_URL,
        open: false,
    })
}
```

## Conclusion

This was just a quick example of **how to use env variables in javascript files**.

It already has an example of how to use it to configure Laravel Mix `browserSync` feature to get hot reload,
you can use this `process.env.<key>` syntax on any javascript file that would be process by mix/webpack to get easily configuration values.

If you are new to Laravel, I would recommend checking out this [Introduction to Laravel 7](https://www.youtube.com/watch?v=ZYDBQcnkj38&list=PL_UnIDIwT95Mn-Txakyt5x183aVXdve2R) free course by **DevDojo**.
