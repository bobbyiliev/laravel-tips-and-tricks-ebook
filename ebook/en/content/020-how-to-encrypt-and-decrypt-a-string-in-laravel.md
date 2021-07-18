# How to encrypt and decrypt a string in Laravel

Encryption is the process of encoding information so that it can not be understood or intercepted.

Encryption has been used long ago before computers were invented; actually, the first known evidence dates back to 1900 BC in Egypt. 

Another very popular encryption technique is the [Caesar cipher](https://en.wikipedia.org/wiki/Caesar_cipher). It is one of the simplest techniques, and how it works is each letter of the text is replaced by a specific number of positions down the alphabet.

Laravel, on the other side, provides out-of-the-box encryption, which uses OpenSSL to provide AES-256 encryption so that you don't really have to come up with your own encryption techniques.

In this tutorial, you will learn how to use the Laravel encryption to encrypt text!

Before you start, you would need to have a Laravel application up and running.

I will be using a DigitalOcean Ubuntu Droplet for this demo. If you wish, you can use my affiliate code to get [free $100 DigitalOcean credit](https://m.do.co/c/2a9bba940f39) to spin up your own servers!

If you do not have that yet, you can follow the steps from this tutorial on how to do that:

* [How to Install Laravel on DigitalOcean with 1-Click](https://devdojo.com/bobbyiliev/how-to-install-laravel-on-digitalocean-with-1-click)

Or you could use this awesome script to do the installation:

* [LaraSail](https://devdojo.com/episode/laravel-on-digital-ocean-with-larasail)

## App Key Configuration

Before you get started, you need to make sure that you have an App Key generated. 

If you do not have a key already generated, to do that, you can run the following command:

```
php artisan key:generate
```

The Laravel encryption will still work without a key, but the encrypted values might be insecure.

## Creating a Route

Now that we have our App Key ready let's go ahead and create two routes, one for testing the Laravel encryption and one for testing the Laravel decryption.

To do that, open the `routes/web.php` file and add the following:

```
Route::get('encrypt', EncryptionController@encrypt');

Route::get('decrypt', EncryptionController@decrypt');
```

The first route is the `/encrypt` route, which will generate an encrypted string for us, and the second one will decrypt that string.

With that, let's create the `EncryptionController` controller!

## Creating a Controller

For this example, let's create a new controller called EncryptionController:

```
php artisan make:controller EncryptionController
```

This will create a new controller at: `app/Http/Controllers/EncryptionController.php`. 

Next, open that file in your text editor and first add the `Crypt` facade:

```
use Illuminate\Support\Facades\Crypt;
```

Then let's create two new public methods: one for encrypting a string and one for decrypting that same string called `encrypt` and `decrypt`.

### Ecryption method

Let's start with a simple Encryption method which would encrypt a hardcoded string for us:

```
   public function encrypt()
   {
        $encrypted = Crypt::encryptString('Hello DevDojo');
        print_r($encrypted);
   }
```

Rundown of the method:

* `public function encrypt()` : first we define the method
* `Crypt::encryptString('Hello DevDojo')` : then using the `Crypt::encryptString()` static method we encrypt a simple `Hello DevDojo` string
* `print_r($encrypted);` : finally, we would print out the encrypted string on the screen.

After that visit, the `/encrypt` URL via your browser and you will see an encrypted string similar to this one:

```
string(188) "eyJpdiI6ImxSdGhkeVg2VHlCNUs0citKT0V4NHc9PSIsInZhbHVlIjoiSEM5V0pVWURySnVabGlnenNwTDgzUT09IiwibWFjIjoiZTJlYWVhYmI2OTJmZWJkZWVhOTg3Nzc1ZTQwNDBlNmI3ODIzZTY5YTgwZGM3N2YwYTRmYTEwYmJiYmNjZmE2NiJ9"
```

Note down this string and go back to your text editor to prepare the `decrypt` method!

### Decryption method

Then create a new public method called `decrypt`:

```
    public function decrypt()
    {
         $decrypt= Crypt::decryptString('your_encrypted_string_here');
         print_r($decrypt);
    }
```

**Note**:
> Make sure to change the `your_encrypted_string_here` with your actual encoded string that you've got from the last step

Similar to the Encrypt method, we are again using the `Crypt` faced with the `decryptString` static method to decrypt the string!

Then this time visits the `/decrypt` URL in your browser, and you will see the decrypted `Hello DevDojo` message!

Of course, the above example is just showing `Crypt` functionality. In a real-life scenario, you would get most likely to get your string from a POST request or an API call for example.

## Conclusion

For more information on how to use Laravel Encryption, make sure to check out the official documentation here:

[https://laravel.com/docs/8.x/encryption](https://laravel.com/docs/8.x/encryption)

[Originally posted here](https://devdojo.com/bobbyiliev/how-to-encrypt-and-decrypt-a-string-in-laravel)