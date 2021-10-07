# How to add a gravatar profile picture in Laravel

Gravatar is a service that allows to use their profile images with external api calls, 
it is another way to handle user profile pictures instead of storing those in the database.

Here a little guide of how we can implement this feature.

* * *

Steps
-----

* Create a trait to add gravatars to any model
* Show a user avatar in blade templates
* Add a gravatar as the default profile picture in jetstream

* * *

## Create a trait to handle the gravatar

You can add a user method or if other models would use the gravatar image you can separate the code into a trait:

```php
namespace App\Traits;

trait HasGravatar {

    /**
     * The attribute name containing the email address.
     *
     * @var string
     */
    public $gravatarEmail = 'email';

    /**
     * Get the model's gravatar
     *
     * @return string
     */
    public function getGravatarAttribute()
    {
        $hash = md5(strtolower(trim($this->attributes[$this->gravatarEmail])));
        return "https://www.gravatar.com/avatar/$hash";
    }

}
```

Now any model can use the trait as User model:

```php 
use App\Traits\HasGravatar;

class User extends Model
{
    use HasGravatar;
}
```

## Render an image in a blade view:

Now you only need to pass a user to the view and use it as below:

```php 
<img src="$user->gravatar" height="150" width="150" />
```

## Use gravatars with Jetstream

If you are working with Jetstream there is a simple way to change the default initial letters to a gravatar.

Just override the method that was originally added to the User model by this trait `Laravel\Jetstream\HasProfilePhoto`

Instead of this:

```php
/**
 * Get the default profile photo URL if no profile photo has been uploaded.
 *
 * @return string
 */
protected function defaultProfilePhotoUrl()
{
    return 'https://ui-avatars.com/api/?name='.urlencode($this->name).'&color=7F9CF5&background=EBF4FF';
}
```

In your User model you can override with this:

```php
/**
 * Get the default profile photo URL if no profile photo has been uploaded.
 *
 * @return string
 */
protected function defaultProfilePhotoUrl()
{
    return $this->getGravatarAttribute();
}
```

## Conclusion

There are is a simple and flexible way to handle how to **add profile avatar images with gravatar in Laravel**.

If you are new to Laravel, I would recommend checking out this [Introduction to Laravel 7](https://www.youtube.com/watch?v=ZYDBQcnkj38&list=PL_UnIDIwT95Mn-Txakyt5x183aVXdve2R) free course by **DevDojo**.
