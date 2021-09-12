# 8 Awesome VS Code Extensions for Laravel Developers

While I'm still a sublime fan for quite some time, I've been mainly using VS Code.

For anyone who is just getting started with Laravel, I would recommend going through this [Laravel basics course here](https://devdojo.com/course/laravel-7-basics)!

Here is a list of my top 8 VS Code extensions for Laravel developers, which would help you be more productive!

## 1. Laravel Blade Snippets

The [Laravel blade snippets](https://marketplace.visualstudio.com/items?itemName=onecentlin.laravel-blade) extension adds syntax highlight support for Laravel Blade to your VS Code editor.

![Visual studio extensions for laravel devs](https://imgur.com/9Q1DDfz.gif)

Some of the main features of this extension are:

* Blade syntax highlight
* Blade snippets
* Emmet works in blade template
* Blade formatting

In order to make sure that the extension works as expected, there is some additional configuration that needs to be done. Go to `File` -> `Preferences` -> `Settings` and add the following to your `settings.json`:

```
"emmet.triggerExpansionOnTab": true,
"blade.format.enable": true,
"[blade]": {
    "editor.autoClosingBrackets": "always"
},
```

This will enable tab completion for emmet tags and if enable blade formatting.

For more information on the available snippets, make sure to check the documentation here:

[VSCode extensions for laravel](https://marketplace.visualstudio.com/items?itemName=onecentlin.laravel-blade)

## 2. Laravel Snippets

This one is probably my personal favorite! The [Laravel Snippets extension](https://marketplace.visualstudio.com/items?itemName=onecentlin.laravel5-snippets) adds snippets for the Facades like `Request::`, `Route::` etc.

![Laravel extensions for VScode](https://imgur.com/Npm1yYE.gif)

Some of the supported snippet prefixes include:

* Auth
* Broadcast
* Cache
* Config
* Console
* Cookie
* Crypt
* DB
* Event
* View

For more information on the available snippets, make sure to check the documentation here:

[VSCode extensions for laravel](https://marketplace.visualstudio.com/items?itemName=onecentlin.laravel5-snippets)

## 3. Laravel Blade Spacer

Isn't it annoying when you try to echo out something in your Blade views with `{{ }}` and your whole line going back 4 spaces? Well, luckily, the [Laravel Blade Spacer](https://marketplace.visualstudio.com/items?itemName=austenc.laravel-blade-spacer) fixes that!

The Laravel blade spacer extension automatically adds spacing to your blade templating markers:

![Laravel blade spacer vs code extension](https://imgur.com/zqbqOVA.gif)

For more information, make sure to check the documentation here:

[VSCode extensions for laravel](https://marketplace.visualstudio.com/items?itemName=austenc.laravel-blade-spacer)

## 4. Laravel Artisan

I personally like to use the command line all the time, but I have to admit that the [Laravel Artisan](https://marketplace.visualstudio.com/items?itemName=ryannaddy.laravel-artisan) extension is awesome! It lets you run Laravel Artisan commands from within Visual Studio Code directly!

![Laravel Artisan VS code extension](https://imgur.com/f6OqmqN.gif)

Some of the main features are:

* Make files like Controllers, Migrations, etc.
* Run Your own Custom Commands
* Manage your database
* Clear the Caches
* Generate Keys
* View all application routes
* Manage your local php server for test purposes

For more information, make sure to check the documentation here:

[VSCode extensions for laravel](https://marketplace.visualstudio.com/items?itemName=ryannaddy.laravel-artisan)

## 5. Laravel Extra Intellisense

The [Laravel Extra Intellisense](https://marketplace.visualstudio.com/items?itemName=amiralizadeh9480.laravel-extra-intellisense) extension provides autocompletion for Laravel in VSCode.

![Laravel autocomplition VScode extension](https://imgur.com/r1ET6Ya.gif)

The extension comes with auto-completion for:

* Route names and route parameters
* Views and variables
* Configs
* Translations and translation parameters
* Laravel mix function
* Validation rules
* View sections and stacks
* Env
* Route Middlewares

For more information, make sure to check the documentation here:

[VSCode extensions for laravel](https://marketplace.visualstudio.com/items?itemName=amiralizadeh9480.laravel-extra-intellisense)

## 6. Laravel goto Controller

As your application grows, the number of your Controllers grows as well, so at some point, you might end up with hundreds of controllers. Hance finding your way around might get tedious.

This is the exact problem that the [Laravel-goto-controller](https://marketplace.visualstudio.com/items?itemName=stef-k.laravel-goto-controller) VScode extension solves.

The extension allows you to press `Alt` + click on the name of the controller in your routes file, and it will navigate you from the route to the respective controller file:

![Laravel goto Controller vscode extension](https://imgur.com/E3h6GwT.png)

For more information, make sure to check the documentation here:

[VSCode extensions for laravel](https://marketplace.visualstudio.com/items?itemName=stef-k.laravel-goto-controller)

## 7. Laravel goto View

Similar to the Laravel goto Controller extension, the [Laravel goto View VScode extension](https://marketplace.visualstudio.com/items?itemName=codingyu.laravel-goto-view) allows you to go from your Controller or Route to your view. This can save you quite a bit of time!

You can use `Ctrl` or `Alt` + click to jump to the first matched Blade View file:

![Laravel go to view VS code extension](https://imgur.com/PHBRhqq.png)

For more information, make sure to check the documentation here:

[VSCode extensions for laravel](https://marketplace.visualstudio.com/items?itemName=codingyu.laravel-goto-view)

## 8. DotENV syntax highlighting

This one is pretty simple but handy. The [DotENV](https://marketplace.visualstudio.com/items?itemName=mikestead.dotenv) VS Code extension is used to highlight the syntax of your `.env` file, which could be quite handy for spotting some problems:

![VS code dotenv hightlight](https://imgur.com/tYxpMbO.png)

For more information, make sure to check the documentation here:

[VSCode extensions for laravel](https://marketplace.visualstudio.com/items?itemName=mikestead.dotenv)

## Book recommendation

If you are a Laravel fan, make sure to check out the [The Laravel Survival Guide](https://devdojo.com/ebook/laravelsurvivalguide) ebook!

## Conclusion

If you like all those extensions, you can take a look at the [Laravel Extension Pack for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=onecentlin.laravel-extension-pack), where you could get all of the mentioned extensions as 1 bundle!

The only extension not included in the pack is the Laravel Blade Spacer, so make sure to install it separately!

[Originally posted here](https://devdojo.com/bobbyiliev/8-awesome-vs-code-extensions-for-laravel-developers).
