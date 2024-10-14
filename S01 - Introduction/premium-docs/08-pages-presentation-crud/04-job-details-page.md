# Job Details Page

Now we want to do the single job listing page. There is a lot of markup here, so we will be copying and pasting some of it.

Open the `resources/views/jobs/show.blade.php` file. This is our view and we already have access to the job object. We can use this to display the job details.

Open the `_theme_files/job-details.html` file. We are going to copy section by section as opposed to copying the whole file.

Let's start by typing out the grid container. Make the page look like this:

```html
<x-layout>
  <div class="grid grid-cols-1 md:grid-cols-4 gap-6"></div>
</x-layout>
```

Now in the `_theme_files/job-details.html` file, let's copy and paste the job details column `<section>` inside the grid container. It looks like this:

```html
<section class="md:col-span-3">
  <div class="rounded-lg shadow-md bg-white p-3">
    <div class="flex justify-between items-center">
      <a class="block p-4 text-blue-700" href="/jobs.html">
        <i class="fa fa-arrow-alt-circle-left"></i>
        Back To Listings
      </a>
      <div class="flex space-x-3 ml-4">
        <a
          href="/edit"
          class="px-4 py-2 bg-blue-500 hover:bg-blue-600 text-white rounded"
          >Edit</a
        >
        <!-- Delete Form -->
        <form method="POST">
          <button
            type="submit"
            class="px-4 py-2 bg-red-500 hover:bg-red-600 text-white rounded"
          >
            Delete
          </button>
        </form>
        <!-- End Delete Form -->
      </div>
    </div>
    <div class="p-4">
      <h2 class="text-xl font-semibold">Software Engineer</h2>
      <p class="text-gray-700 text-lg mt-2">
        As a Software Engineer at Algorix, you will be responsible for
        designing, developing, and maintaining high-quality software
        applications. You will work closely with cross-functional teams to
        deliver scalable and efficient solutions that meet business needs. The
        role involves writing clean, maintainable code, participating in code
        reviews, and staying current with industry trends to ensure our
        technology stack remains cutting-edge.
      </p>
      <ul class="my-4 bg-gray-100 p-4">
        <li class="mb-2"><strong>Job Type:</strong> Full Time</li>
        <li class="mb-2"><strong>Remote:</strong> No</li>
        <li class="mb-2"><strong>Salary:</strong> $80,000</li>
        <li class="mb-2">
          <strong>Site Location:</strong> New York, NY
          <span
            class="text-xs bg-blue-500 text-white rounded-full px-2 py-1 ml-2"
            >Local</span
          >
        </li>
        <li class="mb-2">
          <strong>Tags:</strong>
          <span>Development</span>,
          <span>Coding</span>
        </li>
      </ul>
    </div>
  </div>

  <div class="container mx-auto p-4">
    <h2 class="text-xl font-semibold mb-4">Job Details</h2>
    <div class="rounded-lg shadow-md bg-white p-4">
      <h3 class="text-lg font-semibold mb-2 text-blue-500">Job Requirements</h3>
      <p>
        Bachelors degree in Computer Science or related field, 3+ years of
        software development experience
      </p>
      <h3 class="text-lg font-semibold mt-4 mb-2 text-blue-500">Benefits</h3>
      <p>Healthcare, 401(k) matching, flexible work hours</p>
    </div>
    <p class="my-5">
      Put "Job Application" as the subject of your email and attach your resume.
    </p>
    <a
      href="mailto:manager@company.com"
      class="block w-full text-center px-5 py-2.5 shadow-sm rounded border text-base font-medium cursor-pointer text-indigo-700 bg-indigo-100 hover:bg-indigo-200"
    >
      Apply Now
    </a>
  </div>

  <div class="bg-white p-6 rounded-lg shadow-md mt-6">
    <div id="map"></div>
  </div>
</section>
```

We are going to ignore the delete button and the map for now. We will come back to those later.

#### Edit Button

We have our resource routes for jobs and we have a controller method that just outputs a string for now, but let's make the edit button link to the edit page. Change the href of the edit button to use the route helper:

```html
<a
  href="{{ route('jobs.edit', $job->id) }}"
  class="px-4 py-2 bg-blue-500 hover:bg-blue-600 text-white rounded"
  >Edit</a
>
```

It takes in the controller method name and the id of the job. This will take us to the edit page.

#### Back Button

Let's change the href of the back link:

```html
<a class="block p-4 text-blue-700" href="{{ route('jobs.index') }}">
  <i class="fa fa-arrow-alt-circle-left"></i>
  Back To Listings
</a>
```

This will take us back to the jobs index page.

#### Job Details

Now let's add the job details like the title, description, etc. Here is the the whole page:

```html
<x-layout>
  <div class="grid grid-cols-1 md:grid-cols-4 gap-6">
    <section class="md:col-span-3">
      <div class="rounded-lg shadow-md bg-white p-3">
        <div class="flex justify-between items-center">
          <a class="block p-4 text-blue-700" href="{{ route('jobs.index') }}">
            <i class="fa fa-arrow-alt-circle-left"></i>
            Back To Listings
          </a>
          <div class="flex space-x-3 ml-4">
            <a
              href="/edit"
              class="px-4 py-2 bg-blue-500 hover:bg-blue-600 text-white rounded"
              >Edit</a
            >
            <!-- Delete Form -->
            <form method="POST">
              <button
                type="submit"
                class="px-4 py-2 bg-red-500 hover:bg-red-600 text-white rounded"
              >
                Delete
              </button>
            </form>
            <!-- End Delete Form -->
          </div>
        </div>
        <div class="p-4">
          <h2 class="text-xl font-semibold">{{$job->title}}</h2>
          <p class="text-gray-700 text-lg mt-2">{{$job->description}}</p>
          <ul class="my-4 bg-gray-100 p-4">
            <li class="mb-2"><strong>Job Type:</strong> {{$job->job_type}}</li>
            <li class="mb-2">
              <strong>Remote:</strong> {{$job->remote ? 'Yes' : 'No'}}
            </li>
            <li class="mb-2">
              <strong>Salary:</strong> ${{ number_format($job->salary) }}
            </li>
            <li class="mb-2">
              <strong>Site Location:</strong> {{$job->city}}, {{$job->state}}
            </li>
            <li class="mb-2">
              <strong>Tags:</strong>
              {{ ucwords(str_replace(',', ', ', $job->tags)) }}
            </li>
          </ul>
        </div>
      </div>

      <div class="container mx-auto p-4">
        <h2 class="text-xl font-semibold mb-4">Job Details</h2>
        <div class="rounded-lg shadow-md bg-white p-4">
          <h3 class="text-lg font-semibold mb-2 text-blue-500">
            Job Requirements
          </h3>
          <p>{{$job->requirements}}</p>
          <h3 class="text-lg font-semibold mt-4 mb-2 text-blue-500">
            Benefits
          </h3>
          <p>{{$job->benefits}}</p>
        </div>
        <p class="my-5">
          Put "Job Application" as the subject of your email and attach your
          resume.
        </p>
        <a
          href="mailto:{{$job->contact_email}}"
          class="block w-full text-center px-5 py-2.5 shadow-sm rounded border text-base font-medium cursor-pointer text-indigo-700 bg-indigo-100 hover:bg-indigo-200"
        >
          Apply Now
        </a>
      </div>

      <div class="bg-white p-6 rounded-lg shadow-md mt-6">
        <div id="map"></div>
      </div>
    </section>
  </div>
</x-layout>
```

Everything is pretty straightforward. We are just outputting the job details from the job object. We are also formatting the salary with the number_format() function so that it shows a comma between every 3 digits. We are also using the ucwords() function to capitalize the first letter of each word in the tags. We used the str_replace() function to replace the commas with commas and spaces.

## Sidebar

Now let's do the sidebar, which will contain the company logo, company name and description as well as a button to bookmark the job.

In the `_theme_files/job-details.html` file, copy the sidebar section:

```html
<aside class="bg-white rounded-lg shadow-md p-3">
  <h3 class="text-xl text-center mb-4 font-bold">Company Info</h3>
  <img
    src="images/logo-algorix.png"
    alt="Ad"
    class="w-full rounded-lg mb-4 m-auto"
  />
  <h4 class="text-lg font-bold">Algorix</h4>
  <p class="text-gray-700 text-lg my-3">
    We are a leading software development company in New York.
  </p>
  <a href="https://sparkle.test" target="_blank" class="text-blue-500"
    >Visit Website</a
  >

  <a
    href=""
    class="mt-10 bg-blue-500 hover:bg-blue-600 text-white font-bold w-full py-2 px-4 rounded-full flex items-center justify-center"
    ><i class="fas fa-bookmark mr-3"></i> Bookmark Listing</a
  >
</aside>
```

Let's replace the company logo, name, description and website with the job object data:

```html
<aside class="bg-white rounded-lg shadow-md p-3">
  <h3 class="text-xl text-center mb-4 font-bold">Company Info</h3>
  <img
    src="/images/{{$job->company_logo}}"
    alt="{{$job->company_name}}"
    class="w-full rounded-lg mb-4 m-auto"
  />
  <h4 class="text-lg font-bold">{{$job->company_name}}</h4>
  <p class="text-gray-700 text-lg my-3">{{$job->company_description}}</p>
  <a href="{{$job->company_website}}" target="_blank" class="text-blue-500"
    >Visit Website</a
  >

  <a
    href=""
    class="mt-10 bg-blue-500 hover:bg-blue-600 text-white font-bold w-full py-2 px-4 rounded-full flex items-center justify-center"
    ><i class="fas fa-bookmark mr-3"></i> Bookmark Listing</a
  >
</aside>
```

Now we have the job details page. We will come back to the edit and delete buttons and the map later. For now, we have a nice looking job details page.
