# Contact Form with Voyager and Laravel

This is an easy step by step guide on how to add a **contact from** to your **Voyager** application.

Before you begin you need to make sure that you have **Laravel** and **Voyager** up and running and that you've sorted out your database connection.

If you are not sure how to do that you can follow the steps here on how to deploy **Laravel** App on **Digital Ocean Ubuntu** server with **Voyager**:

[**devdojo.com**](https://devdojo.com/tutorials/laravel-app-on-digital-ocean-ubuntu-1904-droplet-step-by-step-guide)

If you don't have a Digital Ocean account yet, you can sign up for Digital Ocean and get **$50 free** credit via this link here:

 **[digitalocean.com](https://m.do.co/c/2a9bba940f39)**

* * *

Steps
-----

The steps that we will take are:

*   Create a Table with a Model
*   Configure the Model
*   Create the Routes
*   Create and Configure the Controller
*   Create the Views
*   Configure the Email settings
*   Test the Form

At the end we would be receiving emails sent though our contact form and we would also be able to see those entires in our Voyager admin panel

* * *

Configuration
-------------

Let's start with our configuration! I have a plain Laravel and Voyager installation that I'll be using. You can also implement that on an existing site, but make sure to **back everything up** before following this guide!

### 1\. Create a Table with a Model

Go to your Voyager admin -> Tools -> Database -> Create New Table

![](https://cdn.devdojo.com/posts/images/June2019/Screenshot 2019-06-14 at 16.14.57.png)

Then go ahead and create a BREAD as well so that we could then see our contact form entries via our Voyager admin area:

![](https://cdn.devdojo.com/posts/images/June2019/Screenshot 2019-06-14 at 16.17.40.png)

You can use the default settings, just scroll to the bottom of the page and hit Submit.

![](https://cdn.devdojo.com/posts/images/June2019/Screenshot 2019-06-14 at 16.18.52.png)

* * *

### 2\. Configure the Model

After that we need to make a slight change to the new Contact model that we've created. In the **app/Contact.php** file add the following lines:

```
<?php

namespace App;

use Illuminate\Database\Eloquent\Model;


class Contact extends Model
{
    public $table = 'contact';
    public $fillable = ['name','email','message'];
}
```

### 3\. Create a route

Add the following to your **routes/web.php** file:

```
Route::get('contact', 'ContactController@contact');
Route::post('contact', ['as'=>'contact.store','uses'=>'ContactController@contactPost']);
```

* * *

### 4\. Create and Configure your Controller

You can run the following artisan command to create your Contact Controller:

```
php artisan make:controller ContactController
```

Then in the **app/Http/Controllers/ContactController.php** file add the following code:

```
<?php
namespace App\Http\Controllers;
use Illuminate\Http\Request;
use App\Http\Requests;
use App\Contact;
use Mail;
class ContactController extends Controller
{
    public function contact()
{
return view('contact');
} 
    /** * Show the application dashboard. * * @return \Illuminate\Http\Response */
    public function contactPost(Request $request) 
    {
    $this->validate($request, [ 'name' => 'required', 'email' => 'required|email', 'message' => 'required' ]);
    Contact::create($request->all());

    Mail::send('email',
        array(
            'name' => $request->get('name'),
            'email' => $request->get('email'),
            'bodyMessage' => $request->get('message')
        ), function($message)
    {
        $message->from('bobby@bobbyiliev.com');
        $message->to('bobby@bobbyiliev.com', 'Bobby')->subject('Bobby Site Contect Form');
    });
    return back()->with('success', 'Thank you for contacting me!'); 
    }
}
```

* * *

### 5\. Create the View

With all that out of the way we can now go ahead and create our view.  In your **resources/views/**  create a file called contact.blade.php and add this code:

```
<!DOCTYPE html>
<html>
<head>
<title>DevDojo - Bobby Iliev - Contact Form</title>
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css">
</head>
<body>

<div class="container">
<h1>Contact Me</h1>

@if(Session::has('success'))
    <div class="alert alert-success">
        {{ Session::get('success') }}
    </div>
@endif

{!! Form::open(['route'=>'contact.store']) !!}

<div class="form-group {{ $errors->has('name') ? 'has-error' : '' }}">
    {!! Form::label('Name:') !!}
    {!! Form::text('name', old('name'), ['class'=>'form-control', 'placeholder'=>'Name']) !!}
<span class="text-danger">{{ $errors->first('name') }}</span>
</div>

<div class="form-group {{ $errors->has('email') ? 'has-error' : '' }}">
    {!! Form::label('Email:') !!}
    {!! Form::text('email', old('email'), ['class'=>'form-control', 'placeholder'=>'Email']) !!}
<span class="text-danger">{{ $errors->first('email') }}</span>
</div>

<div class="form-group {{ $errors->has('message') ? 'has-error' : '' }}">
    {!! Form::label('Message:') !!}
    {!! Form::textarea('message', old('message'), ['class'=>'form-control', 'placeholder'=>'Message']) !!}
<span class="text-danger">{{ $errors->first('message') }}</span>
</div>

<div class="form-group">
<button class="btn btn-success">Send mail</button>
</div>

{!! Form::close() !!}

</div>

</body>
</html>
```

Do not forget to install the **laravelcollective/html** package otherwise your form would not work:

```
composer require laravelcollective/html
```

This is a simple **Bootstrap** form that would look something like this, of course you can customize that so that it meets your requirements:

![](https://cdn.devdojo.com/posts/images/June2019/Screenshot 2019-06-14 at 16.55.00.png)

Let's take care of the email view as well. This would be the actual email that would be send out each time someone uses our form. Again in the **resources/views/** add a file called email.blade.php with the following content:

```
Contact from enquery from: {{ $name }}
<p> Name: {{ $name }} </p>
<p> Email: {{ $email }} </p>
<p> Message: {{ $bodyMessage }} </p>
```

* * *

### 6\. Configure the Email settings

I'll be using **SMTP** to send out the emails, so what I would need to do is to configure the basic **Laravel** mail function through PHP **Artisan**:

    php artisan make:mail smtp

Then in your **.env** file specify your SMTP settings:

```
MAIL_DRIVER=smtp
MAIL_HOST=smtp.gmail.com
MAIL_PORT=587
MAIL_USERNAME=your_email_here@gmail.com
MAIL_PASSWORD=your_password_here
MAIL_ENCRYPTION=tls
```

* * *

### 7\. Test the Form

With all that sorted out we are ready to test our form!

![](https://cdn.devdojo.com/posts/images/June2019/Screenshot 2019-06-14 at 16.59.23.png)

![](https://cdn.devdojo.com/posts/images/June2019/Screenshot 2019-06-14 at 17.07.12.png)

You would also be able to see your emails via your **Voyager** Admin panel:

![](https://cdn.devdojo.com/posts/images/June2019/Screenshot 2019-06-14 at 17.11.16.png)

* * *

Conclusion
----------

That's pretty much it! It is pretty straight forward but always make sure to backup your website before making any chances :)

[Originally posted here](https://devdojo.com/bobbyiliev/contact-form-with-voyager-and-laravel)