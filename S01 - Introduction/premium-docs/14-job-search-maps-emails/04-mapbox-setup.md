# Mapbox Setup

Now I want to show a map with a marker on the job listing pages. We will use the address and other location fields in the database.

## Create a Mapbox Account

First, you need to create a Mapbox account. Go to [Mapbox](https://www.mapbox.com/) and sign up for a free account. Go to https://account.mapbox.com/ and copy you API key.

Open your `.env` file and add the following:

```bash
MAPBOX_API_KEY=YOUR_KEY
```

We are going to add a script tag directly into our show view. Open the `app/views/jobs/show.blade.php` file and add the following at the very bottom of the file:

```html
<link
  href="https://api.mapbox.com/mapbox-gl-js/v2.7.0/mapbox-gl.css"
  rel="stylesheet"
/>
<script src="https://api.mapbox.com/mapbox-gl-js/v2.7.0/mapbox-gl.js"></script>
<script>
  document.addEventListener('DOMContentLoaded', function () {
    // Your Mapbox access token
    mapboxgl.accessToken = "{{ env('MAPBOX_API_KEY') }}";

    // Initialize the map
    const map = new mapboxgl.Map({
      container: 'map', // ID of the container element
      style: 'mapbox://styles/mapbox/streets-v11', // Map style
      center: [-74.5, 40], // Default center
      zoom: 9, // Default zoom level
    });

    // Get address from Laravel view
    const city = '{{ $job->city }}';
    const state = '{{ $job->state }}';
    const address = city + ', ' + state;

    // Geocode the address
    fetch(
      `https://api.mapbox.com/geocoding/v5/mapbox.places/${encodeURIComponent(
        address
      )}.json?access_token=${mapboxgl.accessToken}`
    )
      .then((response) => response.json())
      .then((data) => {
        if (data.features.length > 0) {
          const [longitude, latitude] = data.features[0].center;

          // Center the map and add a marker
          map.setCenter([longitude, latitude]);
          map.setZoom(14);

          new mapboxgl.Marker().setLngLat([longitude, latitude]).addTo(map);
        } else {
          console.error('No results found for the address.');
        }
      })
      .catch((error) => console.error('Error geocoding address:', error));
  });
</script>
```

This script will initialize the map and add a marker to the location of the job. It will geocode the address and get the latitude and longitude to center the map and add a marker.

We need to add a tiny bit of CSS. Open the `public/css/style.css` file and add the following:

```css
#applicant-form {
  position: relative;
  z-index: 2;
}

#map {
  z-index: 1;
  height: 400px;
}
```

This will give the map a height so it shows and it will make sure the applicant form is on top of the map.

The map should now show, which is good, however, your mapbox key is public and anyone can see it. We need to do a bit more work if you want to hide this from the public. We will do that next.
