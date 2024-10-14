# Request Object & Query Params

In Laravel, you can access the request object in a route closure. The request object contains all the information about the request including the following:

- Request method (GET, POST, PUT, DELETE, etc.)
- Request URI
- Request headers
- Request body
- Query parameters
- Form data
- Uploaded files
- Cookies
- Session data

To access the request object, you can type-hint it in the closure like so:

```php
Route::get('/test', function (Illuminate\Http\Request $request) {
    return $request;
});
```

The reason we add the type-hinting is because Laravel automatically includes something called dependecy injection when we do so. By specifying `Illuminate\Http\Request  $request`, Laravel knows that it needs to pass an instance of Illuminate\Http\Request into the method. Without the type hint, Laravel wouldn't know which object to inject. It would be treated as a generic variable.

However, you probably don't want to include the entire namespace every time you want to access the request object. Instead, you can import the `Request` class at the top of the file like so:

```php
use Illuminate\Http\Request;
```

Then you can access the request object like this:

```php
Route::get('/test', function (Request $request) {
    return $request;
});
```

There are many methods to access various parts of the request object. Here are a few examples:

- `$request->method()` - Get the request method (GET, POST, PUT, DELETE, etc.)
- `$request->url()` - Get the request URL
- `$request->header('Content-Type')` - Get a request header
- `$request->all()` - Get all request data (query parameters, form data, etc.)
- `$request->query('name')` - Get a query parameter by name
- `$request->input('name')` - Get a form input by name
- `$request->file('photo')` - Get an uploaded file by name
- `$request->cookie('name')` - Get a cookie by name
- `$request->session()->get('key')` - Get a session value by key

Let's check out some of this stuff in action.

```php
Route::get('/test', function (Illuminate\Http\Request $request) {
    return [
        'method' => $request->method(),
        'url' => $request->url(),
        'path' => $request->path(),
        'fullUrl' => $request->fullUrl(),
        'ip' => $request->ip(),
        'userAgent' => $request->userAgent(),
        'header' => $request->header(),
    ];
});
```

## Query Parameters

Here is an example of accessing query parameters:

```php
Route::get('/user', function (Request $request) {
    return $request->query('name');
});
```

Now visit `http://localhost:8000/user?name=John` and you will see the string `John`.

### Multiple Query Parameters

You can also get multiple query parameters like so:

```php
Route::get('/user', function (Request $request) {
    return $request->only(['name', 'age']);
});
```

Now visit `http://localhost:8000/user?name=John&age=30` and you will see `{"name":"John","age":"30"}`.

### $request->input

You can also use `$request->input('name')` to get query parameters. The difference between `query` and `input` is that `query` only gets query parameters, while `input` gets both query parameters and form data.

To get all query parameters, you can use the `all` method:

```php
Route::get('/user', function (Request $request) {
    return $request->all();
});
```

### Check if Query Parameter Exists

You can also check if a query parameter exists like so:

```php
Route::get('/user', function (Request $request) {
    return $request->has('name');
});
```

Now visit `http://localhost:8000/user?name=John` and you will see `true`. If you visit `http://localhost:8000/user`, you will see `false`.

### Default Value

You can also provide a default value if the query parameter doesn't exist:

```php
Route::get('/user', function (Request $request) {
    return $request->input('name', 'Default Name');
});
```

Now if you visit `http://localhost:8000/user?name=John`, you will see `John`. If you visit `http://localhost:8000/user`, you will see `Default Name`.


You can also exclude query parameters like so:

```php
Route::get('/user', function (Request $request) {
    return $request->except(['name']);
});
```

Now visit `http://localhost:8000/user?name=John&age=30` and you will see `{"age":"30"}`.
