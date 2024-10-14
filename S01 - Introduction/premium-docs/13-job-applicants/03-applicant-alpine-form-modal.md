# Applicant Alpine Form Modal

In this section, we will create a form to allow applicants to submit their job applications. We are going to use Alpine.js to show a form modal.

Open the file `resources/views/jobs/show.blade.php` and find this code:

```html
<p class="my-5">
  Put "Job Application" as the subject of your email and attach your resume.
</p>
<a
  href="mailto:{{$job->contact_email}}"
  class="block w-full text-center px-5 py-2.5 shadow-sm rounded border text-base font-medium cursor-pointer text-indigo-700 bg-indigo-100 hover:bg-indigo-200"
>
  Apply Now
</a>
```

Replace this with the following code:

```html
<!-- Applicant Form -->
<div x-data="{ open: false }" id="applicant-form">
  <button
    @click="open = true"
    class="block w-full text-center px-5 py-2.5 mt-5 shadow-sm rounded border text-base font-medium cursor-pointer text-indigo-700 bg-indigo-100 hover:bg-indigo-200"
  >
    Apply Now
  </button>

  <div
    x-show="open"
    class="fixed inset-0 flex items-center justify-center bg-gray-900 bg-opacity-50"
  >
    <div @click.away="open = false" class="bg-white p-6 rounded-lg shadow-md w-full max-w-md">
      <h3 class="text-lg font-semibold mb-4">Apply for {{ $job->title }}</h3>

      <form enctype="multipart/form-data">
         <x-inputs.text id="full_name" name="full_name" label="Full Name" :required="true" />
          <x-inputs.text id="contact_phone" name="contact_phone" label="Contact Phone" />
          <x-inputs.text id="contact_email" name="contact_email" label="Contact Email" :required="true" />
          <x-inputs.text-area id="message" name="message" label="Message" />
          <x-inputs.text id="location" name="location" label="Location" />
          <x-inputs.file id="resume" name="resume" label="Upload Your Resume (pdf)" :required="true" />
          <button
            type="submit"
            class="bg-blue-500 hover:bg-blue-600 text-white px-4 py-2 rounded-md"
          >
            Submit Application
          </button>
          <button
            type="button"
            @click="open = false"
            class="ml-2 bg-gray-300 hover:bg-gray-400 text-black px-4 py-2 rounded-md"
          >
            Cancel
          </button>
      </form>
    </div>
  </div>
</div>
```

Add the `required` prop to the text and file components:

```php
@props(['id', 'name', 'label' => null, 'type' => 'text', 'value' => '', 'placeholder' => '', 'required' => false])

<div class="mb-4">
    @if($label)
    <label class="block text-gray-700" for="{{$id}}">{{$label}}</label>
    @endif
    <input id="{{$id}}" type="{{$type}}" name="{{$name}}"
        class="w-full px-4 py-2 border rounded focus:outline-none @error($name) border-red-500 @enderror"
        placeholder="{{$placeholder}}" value="{{old($name, $value)}}" {{$required ? 'required' : '' }} />
    @error($name)
    <p class="text-red-500 text-sm mt-1">{{$message}}</p>
    @enderror
</div>
```

```php
@props(['id', 'name', 'label' => null, 'required' => false])

<div class="mb-4">
    @if($label)
    <label class="block text-gray-700" for="{{$id}}">{{$label}}</label>
    @endif
    <input {{$required ? 'required' : '' }} id="{{$id}}" type="file" name="{{$name}}"
        class="w-full px-4 py-2 border rounded focus:outline-none @error($name) border-red-500 @enderror" />
    @error($name)
    <p class="text-red-500 text-sm mt-1">{{$message}}</p>
    @enderror
</div>
```

We are using Alpine.js to create a modal form for the job application. When the "Apply Now" button is clicked, the form will be displayed as a modal. The form includes fields for the applicant's full name, contact number, contact email, message, location, and resume upload. The form also includes a submit button to submit the application and a cancel button to close the form.

Let's add the action to the form. Update the form tag to include the action attribute and pass in the route and job ID:

```html
<form
  action="{{ route('applicants.store', $job->id) }}"
  method="POST"
  enctype="multipart/form-data"
></form>
```

This will raise an error because the route does not exist yet. We will create the route in the next section along with the controller method.
