## Policy & Authorization In Controller

Right now, the policy is only preventing the user from seeing the edit and delete buttons. We need to use the policy in the job controller so they actually can't update or delete unless they own the listing.

Open the file `app/Http/Controllers/JobController.php` and add the following import:

```php
use Illuminate\Foundation\Auth\Access\AuthorizesRequests;
```

We also need to add the following to the class:

```php
class JobController extends Controller
{
    use AuthorizesRequests;

// ...rest of the class
}
```

This will make the `AuthorizedRequests` trait available to the class. So we can use methods like `authorize` and `authorizeForUser` in the controller.

Now, let's add the following code to the `update` method:

```php
public function update(Request $request,  Job $job): RedirectResponse
{
    // Check if the user is authorized
    $this->authorize('update', $job);

    // ...rest of the method
}
```

Add the following code to the `destroy` method:

```php
 public function destroy(Job $job): RedirectResponse
{
    // Check if the user is authorized
    $this->authorize('delete', $job);
    // ...rest of the method
}
```

Now if you try and edit or delete a listing that you don't own, you will get a 403 error.

## Prevent User From Seeing The Edit Form

We also need to prevent the user from seeing the edit form if they don't own the listing. Open the file `app/Http/Controllers/JobController.php` and add the following code to the `edit` method:

```php
public function edit(Job $job): View
{
    // Check if the user is authorized
    $this->authorize('update', $job);
    // ...rest of the method
}
```

Now they can not even see the form if they don't own the listing.

That is it as far as the authorization goes for job listings.
