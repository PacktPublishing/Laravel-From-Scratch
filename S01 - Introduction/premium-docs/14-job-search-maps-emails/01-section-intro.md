# Job Search, Maps & Emails

Alright guys, we're almost there. We're going to do three things in this section. First, we'll add the job search functionality. We'll make the form that is in the Hero it's own search component. We'll also show that component on the jobs page. We'll have a route to submit to that will filter the jobs by keyword and location.

Next, we'll be implementing the Mapbox library to show a simple map on the details page with a marker for the location. We need to use geocoding to do this, which Mapbox provides. We do have the issue of the Mapbox API key. Initially, we'll add it to the JavaScript on the client, but that isn't the best thing to do because users can see that. So we'll create a geocode controller in Laravel with a route that we can hit from the client so that the API key is stored on the server.

Finally, we will set up emails so that when a job is applied to, the owner will get an email telling them. The email will also have the data and a download attachment for the resume. We will be using a service called Mailtrap for this. You don't have to pay anything because they have a generous free tier. 