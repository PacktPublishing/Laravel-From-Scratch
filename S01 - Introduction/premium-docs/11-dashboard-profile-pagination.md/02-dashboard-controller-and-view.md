# Dashboard Controller and View

The dashboard page will have a form with the user's name and email. The user can update their name and email from this form by submitting to the profile controller method, which we will update soon. It will also have the user's job listings and any applicant submissions to those job listings.

## Dashboard Controller

Let's create a new controller for the dashboard:

```bash
php artisan make:controller DashboardController
```

Add an index method to the controller:

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use Illuminate\Support\Facades\Auth;
use App\Models\Job;
use Illuminate\View\View;

class DashboardController extends Controller
{
    public function index(Request $request): View
    {
        // Get the authenticated user
        $user = Auth::user();

        // Get all job listings for the authenticated user
        $jobs = Job::where('user_id', $user->id)->get();

        return view('dashboard', compact('user', 'jobs'));
    }
}

```

We get the user and all job listings for the authenticated user. We then pass the user and jobs to the view.

## Dashboard Route

Let's add our route. Open the `routes/web.php` file and add the following import:

```php
use App\Http\Controllers\DashboardController;
```

Add the route and apply the `auth` middleware:

```php
Route::get('/dashboard', [DashboardController::class, 'index'])->name('dashboard')->middleware('auth');
```

## Profile View

Create a new view in the `resources/views/dashboard` directory called `index.blade.php`. Add the following content:

```html
<x-layout> Dashboard </x-layout>
```

Make sure that the page shows when you go to `/dashboard`. There should already be a link to the dashboard page in the navigation bar.

In the next lesson, we will add the form to update the user's name and email.
