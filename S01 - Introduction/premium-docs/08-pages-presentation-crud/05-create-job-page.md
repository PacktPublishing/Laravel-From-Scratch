# Create Job Page

Right now our create page looks horrible and only has a title and description field.

Let's open the `/resources/views/jobs/create.blade.php` file as well as the `_theme_files/create-job.html` file. Copy the entire `<div>` within the `<main>` tag in the theme file and paste it inside of the `<x-layout>` tags in the `/resources/views/jobs/create.blade.php` file. Forget the stuff we had there. We will re-add it where we need it.

The page should look like this at the moment:

```html
<x-layout>
  <div class="bg-white mx-auto p-8 rounded-lg shadow-md w-full md:max-w-3xl">
    <h2 class="text-4xl text-center font-bold mb-4">Create Job Listing</h2>
    <form method="POST" action="/jobs" enctype="multipart/form-data">
      <h2 class="text-2xl font-bold mb-6 text-center text-gray-500">
        Job Info
      </h2>

      <div class="mb-4">
        <label class="block text-gray-700" for="title">Job Title</label>
        <input
          id="title"
          type="text"
          name="title"
          class="w-full px-4 py-2 border rounded focus:outline-none"
          placeholder="Software Engineer"
        />
      </div>

      <div class="mb-4">
        <label class="block text-gray-700" for="description"
          >Job Description</label
        >
        <textarea
          cols="30"
          rows="7"
          id="description"
          name="description"
          class="w-full px-4 py-2 border rounded focus:outline-none"
          placeholder="We are seeking a skilled and motivated Software Developer to join our growing development team. In this role, you will be responsible for designing, developing, and maintaining high-quality software solutions that meet our clients' needs. You will work closely with cross-functional teams to deliver robust applications and improve existing systems."
        ></textarea>
      </div>

      <div class="mb-4">
        <label class="block text-gray-700" for="salary">Annual Salary</label>
        <input
          id="salary"
          type="text"
          name="salary"
          class="w-full px-4 py-2 border rounded focus:outline-none"
          placeholder="90000"
        />
      </div>

      <div class="mb-4">
        <label class="block text-gray-700" for="requirements"
          >Requirements</label
        >
        <textarea
          id="requirements"
          name="requirements"
          class="w-full px-4 py-2 border rounded focus:outline-none"
          placeholder="Bachelor's degree in Computer Science"
        ></textarea>
      </div>

      <div class="mb-4">
        <label class="block text-gray-700" for="benefits">Benefits</label>
        <textarea
          id="benefits"
          name="benefits"
          class="w-full px-4 py-2 border rounded focus:outline-none"
          placeholder="Health insurance, 401k, paid time off"
        ></textarea>
      </div>

      <div class="mb-4">
        <label class="block text-gray-700" for="tags"
          >Tags (comma-separated)</label
        >
        <input
          id="tags"
          type="text"
          name="tags"
          class="w-full px-4 py-2 border rounded focus:outline-none"
          placeholder="development,coding,java,python"
        />
      </div>

      <div class="mb-4">
        <label class="block text-gray-700" for="job_type">Job Type</label>
        <select
          id="job_type"
          name="job_type"
          class="w-full px-4 py-2 border rounded focus:outline-none"
        >
          <option value="Full-Time" selected>Full-Time</option>
          <option value="Part-Time">Part-Time</option>
          <option value="Contract">Contract</option>
          <option value="Temporary">Temporary</option>
          <option value="Internship">Internship</option>
          <option value="Volunteer">Volunteer</option>
          <option value="On-Call">On-Call</option>
        </select>
      </div>

      <div class="mb-4">
        <label class="block text-gray-700" for="remote">Remote</label>
        <select
          id="remote"
          name="remote"
          class="w-full px-4 py-2 border rounded focus:outline-none"
        >
          <option value="false">No</option>
          <option value="true">Yes</option>
        </select>
      </div>

      <div class="mb-4">
        <label class="block text-gray-700" for="address">Address</label>
        <input
          id="address"
          type="text"
          name="address"
          class="w-full px-4 py-2 border rounded focus:outline-none"
          placeholder="123 Main St"
        />
      </div>

      <div class="mb-4">
        <label class="block text-gray-700" for="city">City</label>
        <input
          id="city"
          type="text"
          name="city"
          class="w-full px-4 py-2 border rounded focus:outline-none"
          placeholder="Albany"
        />
      </div>

      <div class="mb-4">
        <label class="block text-gray-700" for="state">State</label>
        <input
          id="state"
          type="text"
          name="state"
          class="w-full px-4 py-2 border rounded focus:outline-none"
          placeholder="NY"
        />
      </div>

      <div class="mb-4">
        <label class="block text-gray-700" for="zipcode">ZIP Code</label>
        <input
          id="zipcode"
          type="text"
          name="zipcode"
          class="w-full px-4 py-2 border rounded focus:outline-none"
          placeholder="12201"
        />
      </div>

      <h2 class="text-2xl font-bold mb-6 text-center text-gray-500">
        Company Info
      </h2>

      <div class="mb-4">
        <label class="block text-gray-700" for="company_name"
          >Company Name</label
        >
        <input
          id="company_name"
          type="text"
          name="company_name"
          class="w-full px-4 py-2 border rounded focus:outline-none"
          placeholder="Company name"
        />
      </div>

      <div class="mb-4">
        <label class="block text-gray-700" for="company_description"
          >Company Description</label
        >
        <textarea
          id="company_description"
          name="company_description"
          class="w-full px-4 py-2 border rounded focus:outline-none"
          placeholder="Company Description"
        ></textarea>
      </div>

      <div class="mb-4">
        <label class="block text-gray-700" for="company_website"
          >Company Website</label
        >
        <input
          id="company_website"
          type="text"
          name="company_website"
          class="w-full px-4 py-2 border rounded focus:outline-none"
          placeholder="Enter website"
        />
      </div>

      <div class="mb-4">
        <label class="block text-gray-700" for="contact_phone"
          >Contact Phone</label
        >
        <input
          id="contact_phone"
          type="text"
          name="contact_phone"
          class="w-full px-4 py-2 border rounded focus:outline-none"
          placeholder="Enter phone"
        />
      </div>

      <div class="mb-4">
        <label class="block text-gray-700" for="contact_email"
          >Contact Email</label
        >
        <input
          id="contact_email"
          type="email"
          name="contact_email"
          class="w-full px-4 py-2 border rounded focus:outline-none"
          placeholder="Email where you want to receive applications"
        />
      </div>

      <div class="mb-4">
        <label class="block text-gray-700" for="company_logo"
          >Company Logo</label
        >
        <input
          id="company_logo"
          type="file"
          name="company_logo"
          class="w-full px-4 py-2 border rounded focus:outline-none"
        />
      </div>

      <button
        type="submit"
        class="w-full bg-green-500 hover:bg-green-600 text-white px-4 py-2 my-3 rounded focus:outline-none"
      >
        Save
      </button>
    </form>
  </div>
</x-layout>
```

There are a few things that we need to add here.

- @csrf - this is a security feature to prevent cross-site request forgery attacks.
- Set the action to /jobs/store
- Add the @error directive to each input field to display the error message if there is one.
- Add the `old()` function to each input field to prefill the input field with the old value if there is one.

## More About @csrf

We added this directive a while ago, but I didn't really explain it and I want to explain it now.

The @csrf directive is a built-in directive that adds a hidden input field to the form with the value of the CSRF token. This is a security feature to prevent cross-site request forgery attacks. This is a type of attack where a malicious website can trick a user into performing actions on another website where the user is authenticated. The attacker can trick the user into submitting a form that performs an action on the other website. The CSRF token is a unique token that is generated for each session and is used to verify that the form submission is coming from the correct website. So this is essential for security.

Alright, here is the next version of the form:

```html
<x-layout>
  <div class="bg-white mx-auto p-8 rounded-lg shadow-md w-full md:max-w-3xl">
    <h2 class="text-4xl text-center font-bold mb-4">Create Job Listing</h2>

    <!-- Form Start -->
    <form method="POST" action="{{ route('jobs.store') }}" enctype="multipart/form-data">
      @csrf

      <h2 class="text-2xl font-bold mb-6 text-center text-gray-500">Job Info</h2>

      <!-- Job Title -->
      <div class="mb-4">
        <label class="block text-gray-700" for="title">Job Title</label>
        <input id="title" type="text" name="title" value="{{ old('title') }}"
          class="w-full px-4 py-2 border rounded focus:outline-none @error('title') border-red-500 @enderror"
          placeholder="Software Engineer" />
        @error('title')
          <p class="text-red-500 text-sm mt-1">{{ $message }}</p>
        @enderror
      </div>

      <!-- Job Description -->
      <div class="mb-4">
        <label class="block text-gray-700" for="description">Job Description</label>
        <textarea cols="30" rows="7" id="description" name="description"
          class="w-full px-4 py-2 border rounded focus:outline-none @error('description') border-red-500 @enderror"
          placeholder="We are seeking a skilled and motivated Software Developer...">{{ old('description') }}</textarea>
        @error('description')
          <p class="text-red-500 text-sm mt-1">{{ $message }}</p>
        @enderror
      </div>

      <!-- Annual Salary -->
      <div class="mb-4">
        <label class="block text-gray-700" for="salary">Annual Salary</label>
        <input id="salary" type="number" name="salary" value="{{ old('salary') }}"
          class="w-full px-4 py-2 border rounded focus:outline-none @error('salary') border-red-500 @enderror"
          placeholder="90000" />
        @error('salary')
          <p class="text-red-500 text-sm mt-1">{{ $message }}</p>
        @enderror
      </div>

      <!-- Requirements -->
      <div class="mb-4">
        <label class="block text-gray-700" for="requirements">Requirements</label>
        <textarea id="requirements" name="requirements"
          class="w-full px-4 py-2 border rounded focus:outline-none @error('requirements') border-red-500 @enderror"
          placeholder="Bachelor's degree in Computer Science">{{ old('requirements') }}</textarea>
        @error('requirements')
          <p class="text-red-500 text-sm mt-1">{{ $message }}</p>
        @enderror
      </div>

      <!-- Benefits -->
      <div class="mb-4">
        <label class="block text-gray-700" for="benefits">Benefits</label>
        <textarea id="benefits" name="benefits"
          class="w-full px-4 py-2 border rounded focus:outline-none @error('benefits') border-red-500 @enderror"
          placeholder="Health insurance, 401k, paid time off">{{ old('benefits') }}</textarea>
        @error('benefits')
          <p class="text-red-500 text-sm mt-1">{{ $message }}</p>
        @enderror
      </div>

      <!-- Tags -->
      <div class="mb-4">
        <label class="block text-gray-700" for="tags">Tags (comma-separated)</label>
        <input id="tags" type="text" name="tags" value="{{ old('tags') }}"
          class="w-full px-4 py-2 border rounded focus:outline-none @error('tags') border-red-500 @enderror"
          placeholder="development,coding,java,python" />
        @error('tags')
          <p class="text-red-500 text-sm mt-1">{{ $message }}</p>
        @enderror
      </div>

      <!-- Job Type -->
      <div class="mb-4">
        <label class="block text-gray-700" for="job_type">Job Type</label>
        <select id="job_type" name="job_type"
          class="w-full px-4 py-2 border rounded focus:outline-none @error('job_type') border-red-500 @enderror">
          <option value="Full-Time" {{ old('job_type') == 'Full-Time' ? 'selected' : '' }}>Full-Time</option>
          <option value="Part-Time" {{ old('job_type') == 'Part-Time' ? 'selected' : '' }}>Part-Time</option>
          <option value="Contract" {{ old('job_type') == 'Contract' ? 'selected' : '' }}>Contract</option>
          <option value="Temporary" {{ old('job_type') == 'Temporary' ? 'selected' : '' }}>Temporary</option>
          <option value="Internship" {{ old('job_type') == 'Internship' ? 'selected' : '' }}>Internship</option>
          <option value="Volunteer" {{ old('job_type') == 'Volunteer' ? 'selected' : '' }}>Volunteer</option>
          <option value="On-Call" {{ old('job_type') == 'On-Call' ? 'selected' : '' }}>On-Call</option>
        </select>
        @error('job_type')
          <p class="text-red-500 text-sm mt-1">{{ $message }}</p>
        @enderror
      </div>

      <!-- Remote -->
      <div class="mb-4">
        <label class="block text-gray-700" for="remote">Remote</label>
        <select id="remote" name="remote"
          class="w-full px-4 py-2 border rounded focus:outline-none @error('remote') border-red-500 @enderror">
          <option value="0" {{ old('remote')==false ? 'selected' : '' }}>No</option>
          <option value="1" {{ old('remote')==true ? 'selected' : '' }}>Yes</option>
        </select>
        @error('remote')
          <p class="text-red-500 text-sm mt-1">{{ $message }}</p>
        @enderror
      </div>

      <h2 class="text-2xl font-bold mb-6 text-center text-gray-500">Company Info</h2>

      <!-- Address -->
      <div class="mb-4">
        <label class="block text-gray-700" for="address">Address</label>
        <input id="address" type="text" name="address" value="{{ old('address') }}"
          class="w-full px-4 py-2 border rounded focus:outline-none @error('address') border-red-500 @enderror"
          placeholder="123 Main St" />
        @error('address')
          <p class="text-red-500 text-sm mt-1">{{ $message }}</p>
        @enderror
      </div>

      <!-- City -->
      <div class="mb-4">
        <label class="block text-gray-700" for="city">City</label>
        <input id="city" type="text" name="city" value="{{ old('city') }}"
          class="w-full px-4 py-2 border rounded focus:outline-none @error('city') border-red-500 @enderror"
          placeholder="Albany" />
        @error('city')
          <p class="text-red-500 text-sm mt-1">{{ $message }}</p>
        @enderror
      </div>

      <!-- State -->
      <div class="mb-4">
        <label class="block text-gray-700" for="state">State</label>
        <input id="state" type="text" name="state" value="{{ old('state') }}"
          class="w-full px-4 py-2 border rounded focus:outline-none @error('state') border-red-500 @enderror"
          placeholder="NY" />
        @error('state')
          <p class="text-red-500 text-sm mt-1">{{ $message }}</p>
        @enderror
      </div>

      <!-- ZIP Code -->
      <div class="mb-4">
        <label class="block text-gray-700" for="zipcode">ZIP Code</label>
        <input id="zipcode" type="text" name="zipcode" value="{{ old('zipcode') }}"
          class="w-full px-4 py-2 border rounded focus:outline-none @error('zipcode') border-red-500 @enderror"
          placeholder="12201" />
        @error('zipcode')
          <p class="text-red-500 text-sm mt-1">{{ $message }}</p>
        @enderror
      </div>

      <!-- Company Name -->
      <div class="mb-4">
        <label class="block text-gray-700" for="company_name">Company Name</label>
        <input id="company_name" type="text" name="company_name" value="{{ old('company_name') }}"
          class="w-full px-4 py-2 border rounded focus:outline-none @error('company_name') border-red-500 @enderror"
          placeholder="Company name" />
        @error('company_name')
          <p class="text-red-500 text-sm mt-1">{{ $message }}</p>
        @enderror
      </div>

      <!-- Company Description -->
      <div class="mb-4">
        <label class="block text-gray-700" for="company_description">Company Description</label>
        <textarea id="company_description" name="company_description"
          class="w-full px-4 py-2 border rounded focus:outline-none @error('company_description') border-red-500 @enderror"
          placeholder="Company Description">{{ old('company_description') }}</textarea>
        @error('company_description')
          <p class="text-red-500 text-sm mt-1">{{ $message }}</p>
        @enderror
      </div>

      <!-- Company Website -->
      <div class="mb-4">
        <label class="block text-gray-700" for="company_website">Company Website</label>
        <input id="company_website" type="url" name="company_website" value="{{ old('company_website') }}"
          class="w-full px-4 py-2 border rounded focus:outline-none @error('company_website') border-red-500 @enderror"
          placeholder="Enter website" />
        @error('company_website')
          <p class="text-red-500 text-sm mt-1">{{ $message }}</p>
        @enderror
      </div>

      <!-- Contact Phone -->
      <div class="mb-4">
        <label class="block text-gray-700" for="contact_phone">Contact Phone</label>
        <input id="contact_phone" type="text" name="contact_phone" value="{{ old('contact_phone') }}"
          class="w-full px-4 py-2 border rounded focus:outline-none @error('contact_phone') border-red-500 @enderror"
          placeholder="Enter phone" />
        @error('contact_phone')
          <p class="text-red-500 text-sm mt-1">{{ $message }}</p>
        @enderror
      </div>

      <!-- Contact Email -->
      <div class="mb-4">
        <label class="block text-gray-700" for="contact_email">Contact Email</label>
        <input id="contact_email" type="email" name="contact_email" value="{{ old('contact_email') }}"
          class="w-full px-4 py-2 border rounded focus:outline-none @error('contact_email') border-red-500 @enderror"
          placeholder="Email where you want to receive applications" />
        @error('contact_email')
          <p class="text-red-500 text-sm mt-1">{{ $message }}</p>
        @enderror
      </div>

      <!-- Company Logo -->
      <div class="mb-4">
        <label class="block text-gray-700" for="company_logo">Company Logo</label>
        <input id="company_logo" type="file" name="company_logo"
          class="w-full px-4 py-2 border rounded focus:outline-none @error('company_logo') border-red-500 @enderror" />
        @error('company_logo')
          <p class="text-red-500 text-sm mt-1">{{ $message }}</p>
        @enderror
      </div>

      <!-- Submit Button -->
      <button type="submit"
        class="w-full bg-green-500 hover:bg-green-600 text-white px-4 py-2 my-3 rounded focus:outline-none">
        Save
      </button>
    </form>
    <!-- Form End -->

  </div>
</x-layout>
```

If you submit an empty form, you will see the errors for the title and description because that is all we have handled in the controller method so far. We will add the rest of the fields soon, but I would like to have some components for our form inputs that include the labels and error messages. We will do that in the next lesson.
