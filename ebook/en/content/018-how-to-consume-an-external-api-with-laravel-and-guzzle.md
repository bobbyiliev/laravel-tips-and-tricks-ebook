# How to consume an external API with Laravel and Guzzle

Laravel provides a wrapper for the Guzzle HTTP client. It allows you to quickly make HTTP requests to communicate with external APIs. 

In this tutorial, you will learn how to use the Laravel HTTP Client, and consume an external API and store the data in a database.

Before you start, you would need to have a Laravel application up and running.

I will be using a DigitalOcean Ubuntu Droplet for this demo. If you wish, you can use my affiliate code to [get free $100 DigitalOcean credit](https://m.do.co/c/2a9bba940f39) to spin up your servers!

If you do not have that yet, you can follow the steps from this tutorial on how to do that:

* [How to Install Laravel on DigitalOcean with 1-Click](https://devdojo.com/bobbyiliev/how-to-install-laravel-on-digitalocean-with-1-click)

Or you could use this awesome script to do the installation:

* [LaraSail](https://devdojo.com/episode/laravel-on-digital-ocean-with-larasail)

You would also need a [QuizAPI](https://quizapi.io) account and an API Key.

QuizAPI is a simple REST API that is free for developers, and it provides a large number of different tech related quizzes and questions.

## Creating a new table

Let's start by creating a new table called `questions` where we will store the output of the requests to the QuizAPI.

To create a new table, you could use the following `artisan` command:

```
php artisan make:migration create_questions_table
```

Output:

```
Created Migration: 2021_01_09_192430_create_questions_table
```

This would generate a new migration file for you at:

```
database/migrations/2021_01_09_192430_create_questions_table.php
```

The Laravel migrations will use the `Schema facade to create and modify database tables and` columns. To keep this simple we will only store the question itself and the available answers:

```
        Schema::create('tasks', function (Blueprint $table) {
            $table->bigIncrements('id');
            $table->string('question');
            $table->string('answer_a')->nullable();
            $table->string('answer_b')->nullable();
            $table->string('answer_c')->nullable();
            $table->string('answer_d')->nullable();
            $table->timestamps();
        });
```

After that, to run the migration, use this `artisan` command here:

```
php artisan migrate
```

Output:

```
Migrating: 2021_01_09_192430_create_questions_table
Migrated:  2021_01_09_192430_create_questions_table (0.02 seconds)
```

For more information about Laravel migrations, make sure to check out this post [here](https://devdojo.com/bobbyiliev/how-to-add-a-new-column-to-an-existing-table-in-a-laravel-migration).

## Create the Model

Once we have our `questions` table ready, let's go ahead and add a `Question` model:

```
php artisan make:model Question
```

Output:

```
Model created successfully.
```

## Create the Controller

```
php artisan make:controller QuestionController
```

Output:

```
Controller created successfully.
```

## QuizAPI overview

The URL that we will be hitting on the QuizAPI is the following:

```
https://quizapi.io/api/v1/questions
```

There we need to pass a couple of parameters:

* Our API key, which you can get from here:

[QuizAPI Key](https://quizapi.io/clientarea/settings/token)

* And the number of questions that we want to pull

For more information, make sure to check out the official [QuizAPI documentation](https://quizapi.io/docs/1.0/overview).

The output that you would get will look like this once you hit the API endpoint:

```
[
  {
    "id": 711,
    "question": "Are arrays supported in shell scripts?",
    "description": null,
    "answers": {
      "answer_a": "True",
      "answer_b": "False",
      "answer_c": "Yes but only under certain conditions",
      "answer_d": null,
      "answer_e": null,
      "answer_f": null
    },
    "multiple_correct_answers": "false",
    "correct_answers": {
      "answer_a_correct": "true",
      "answer_b_correct": "false",
      "answer_c_correct": "false",
      "answer_d_correct": "false",
      "answer_e_correct": "false",
      "answer_f_correct": "false"
    },
    "correct_answer": null,
    "explanation": null,
    "tip": null,
    "tags": [
      {
        "name": "BASH"
      },
      {
        "name": "Linux"
      }
    ],
    "category": "Linux",
    "difficulty": "Easy"
  }
]
```

For simplicity, we will want to grab only the question title and the answers from A to D.

Feel free to extend the method and the database table to grab all of the information.

## Building the method

Once we have all that in place, we are ready to start building our method, which will be used to trigger the HTTP requests to the QuizAPI, get a question, and store it in our `questions` table.

With your favorite text editor, open the `QuestionController.php` file at:

```
app/Http/Controllers/QuestionController.php
```

First, make sure to include the Question model:

```
use App\Models\Question;
```

> **Note**: if you are on Laravel 7, you need to use the following instead:

```
use App\Question;
```

After that, also include the HTTP client:

```
use Illuminate\Support\Facades\Http;
```

And then create a new public method called `fetch`, for example:

```
public function fetch()
{

}
```

Inside the `fetch` method, we can start adding our logic:

* First let's make an HTTP request to the QuizAPI questions endpoint:

```
        $response = Http::get('https://quizapi.io/api/v1/questions', [
            'apiKey' => 'YOUR_API_KEY_HERE',
            'limit' => 10,
        ]);
```

With the `Http` client, we are making a `GET` request, and we are hitting the `/api/v1/questions1 endpoint. We are also passing 2 parameters: the API Key and the number of questions that we want to get.

Next, as the output would be in a JSON format we can add use the following to decode it:

```
$quizzes = json_decode($response->body());
```

Then once we have the response body, let's go ahead and use a foreach loop to store the response in our `questions` table:

```
        foreach($quizzes as $quiz){
                $question = new Question;
                $question->question = $quiz->question;
                $question->answer_a = $quiz['answers']->answer_a;
                $question->answer_b = $quiz['answers']->answer_b;
                $question->answer_c = $quiz'answers']->answer_c;
                $question->answer_d = $quiz['answers']->answer_d;
                $question->save();
        }
        return "DONE";
```

The whole `fetch` method will look like this:

```
    public function fetch()
    {
        $response = Http::get('https://quizapi.io/api/v1/questions', [
            'apiKey' => 'YOUR_API_KEY_HERE',
            'limit' => 10,
        ]);
        $quizzes = json_decode($response->body());
        foreach($quizzes as $quiz){
                $question = new Question;
                $question->question = $quiz->question;
                $question->answer_a = $quiz->answers->answer_a;
                $question->answer_b = $quiz->answers->answer_b;
                $question->answer_c = $quiz->answers->answer_c;
                $question->answer_d = $quiz->answers->answer_d;
                $question->save();
        }
        return "DONE";
    }
```

Now let's create a simple route which we will hit and trigger the `fetch` method.

## Add the route

Let's now add the route! To do so, edit the `web.php` file at:

```
routes/web.php
```

And add the following GET route:

```
Route::get('/fetch', 'QuestionController@fetch');
```

Now, if you hit the route and then check your database, you will see 10 new questions in there:

![Laravel Http client](https://imgur.com/9jtTBLQ.png)

## Conclusion

This is pretty much it! Now you know how to use the Laravel HTTP Client to consume an external API and store the information in your database. For more information, make sure to check out the official documentation [here](https://laravel.com/docs/8.x/http-client).

The next step would be to create a view where you could render the data that you've stored in your `questions` table!

[Originally posted here](https://devdojo.com/bobbyiliev/how-to-consume-an-external-api-with-laravel-and-guzzle)