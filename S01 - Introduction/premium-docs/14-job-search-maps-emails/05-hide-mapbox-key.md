# Hide Mapbox Key

Right now our map is showing, but the key is visible. Let's hide it by using a proxy endpoint. We will create a new route that will call the Mapbox API and return the data to the client.

## Create a Proxy Route

Let's create a new route that will call the Mapbox API and return the data to the client. Open the `routes/web.php` file and add the following import:

```php
use App\Http\Controllers\GeocodeController;
```

Now add the following route:

```php
Route::get('/geocode', [GeocodeController::class, 'geocode']);
```

## Create a Controller

Now create a controller with the following command:

```bash
php artisan make:controller GeocodeController
```

Open the `app/Http/Controllers/GeocodeController.php` file and add the following import:

```php
use Illuminate\Support\Facades\Http;
```

Add the following method:

```php
 public function geocode(Request $request): array
{
    $address = $request->input('address');
    $accessToken = env('MAPBOX_API_KEY');

    $response = Http::get("https://api.mapbox.com/geocoding/v5/mapbox.places/{$address}.json", [
        'access_token' => $accessToken
    ]);

    return $response->json();
}
```

What we are going is taking in the address from the request, and then using the `Http` facade to make a GET request to the Mapbox API from the server side. We are passing in the address as a query parameter, and then passing in the access token as a query parameter. We are then returning the response as JSON. This way the key is only on the server side and not the client side.

## Update the Blade File

Now let's update the script in the `/resources/views/jobs/show.blade.php` file. Replace the `fetch` call with the following:

```javascript
 // Call proxy endpoint
fetch(`/geocode?address=${encodeURIComponent(address)}`)
    .then(response => response.json())
    .then(data => {
        if (data.features.length > 0) {
            const [longitude, latitude] = data.features[0].center;

            // Center the map and add a marker
            map.setCenter([longitude, latitude]);
            map.setZoom(14);

            new mapboxgl.Marker()
                .setLngLat([longitude, latitude])
                .addTo(map);
        } else {
            console.error('No results found for the address.');
        }
    })
    .catch(error => console.error('Error geocoding address:', error));
});
```

We are making a request to our own server from the frontend.

Test it out and you should see the map and marker.
