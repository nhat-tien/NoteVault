
source: https://stackoverflow.com/questions/65875215/what-is-the-difference-between-middleware-vs-guards-vs-gates-policies-in-laravel

## Middleware

Typically runs on a route (but you can also run it on controller methods) and can be used to filter or inspect incoming requests.

One example would be auth, which determines if the person trying to request a particular route is authenticated (logged in) to the system. Another example would be to check that a request has a specific header (e.g. if you want to check that the app is sending a X-MYAPP-CUSTOMHEADER header or something)

As mentioned, middleware can be defined on a route (e.g. in web.php or api.php) or in a controller.

An example in web.php:

```php
<?php 

// Get all the posts, but only if the user has signed in to the website 
Route::get('/posts', [PostController::class, 'index'])->middleware('auth');
```

An example in PostController.php:
```php
<?php 

public function __construct() {
    // Apply the `auth` middleware to every function in this controller
    $this->middleware('auth');
    // Apply the `signed` middleware, but only to the functions `download` and `delete`
    $this->middleware('signed', ['only' => ['download', 'delete']]);
}
```

## Gates

Gates are functions defined in your AuthServiceProvider.php file (in the App\Providers folder) and specify what a user is allowed to do and what they're not allowed to do. For example:

```php
<?php 

Gate::define('delete-post', function (User $user, Post $post) {
    return $user->id === $post->user_id;
});
```
Then in your PostController's delete method:
```php
<?php 

public function delete(Request $request, Post $post)
{
    if (Gate::denies('delete-post', $post)) { // Returns true if `$post->user_id` is not the same as `$user->id` (a.k.a the user is not allowed to delete this post)
        abort(403);
    }

    $post->delete();
}
```
You can also use some helper methods in your blade templates:

```blade
@can('delete-post', $post)
    <!-- Show a link to the delete page here -->
@endcan
(I've expanded on this below)
```

## Guards
Guards are a way to specify how users are authenticated for requests.

In a project I'm working on, I have a jwt (JSON Web Token) guard on my API routes. This means that when I do something like `auth()->attempt(['username' => 'test', 'password' => 'test']);`, the auth() function will try and authenticate me using the jwt guard.

Which guard to use is specified in auth.php. Mine currently looks like this:

```php
<?php 

    'guards' => [
        'web' => [
            'driver' => 'session',
            'provider' => 'users',
        ],

        'api' => [
            'driver' => 'jwt',
            'provider' => 'users'
        ],
    ],
```

So in this case, requests coming in via the browser will have a session assigned when they log in, and requests coming in via an API call will need to get / provide a token to authenticate. Both will look up the users table to check the username / password when authenticating.

You can specify which guard to use with the auth() call:

```php
<?php

auth('api')->attempt(['api_key' => 'abc1234'])
```

(and side note, I got caught up with this, as I was wondering why auth()->user() wasn't returning the current user, and that's because web was the default guard, and I was trying to get the user who had authenticated via api, so be sure to be explicit about which guard!)

## Policies

Policies work similarly to gates, but just apply to a specific model and are stored in their own file (in App\Policies)

You can create one by using php artisan make:policy PostPolicy -m Post. It'll create a file called PostPolicy.php which will create a bunch of functions:

```php
<?php 

viewAny // Can the user even look at this model? If no, they'll be denied for all the below methods
view // Can the user look at the specified Post?
create // Can they create a new Post
update // Can they edit / update the specified Post?
delete // Can they (soft) delete the specified Post?
restore // Can they restore the specified (soft) deleted Post?
forceDelete // Can they force delete the specified Post?
```
Typical function(s) would look like this:

```php
<?php 

public function viewAny(User $user)
{
    // If this returns true, then the other methods will be evaluated.
    return $user->can_view_posts;
}

public function forceDelete(User $user, Post $post)
{
    // If this returns true, then the user can force delete the post.
    // This depends on viewAny being true
    return $post->user_id == $user->id;
}
```

One thing to note, is that viewAny is NOT the same as "view all"! Think of viewAny as the front door to a building. If viewAny is true, you can go into the lobby, but you can't look inside any of the rooms unless view for a particular room is also true.

I believe you can also use the `@can` in blade templates with policies:

```blade
@can('forceDelete', $post)
    <!-- Show button to force delete a post here -->
@endcan
And the inverse too:

@cannot('view', $post)
    <!-- Show a greyed out button or something -->
@cannot
As well as the @canany for checking multiple permissions:

@canany(['edit', 'delete'])
    <!-- Show something if the user can edit OR delete -->
@endcanany
```
## Conclusion

I hope this has been useful. I certainly learned a lot while reading up on this. There's way more to this than I thought, so it's worth checking out the Laravel documentation because I may be right in some things, but I may be waaay off in other things.
