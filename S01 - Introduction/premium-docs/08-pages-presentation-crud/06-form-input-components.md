# Form Input Components

So we have our form, but the code is very repetitive. We have a lot of input fields and labels and error messages. We can create a component for inputs like text, textarea, select, etc. This is a good practice because it makes our code more readable and easier to maintain. If you have ever used a frontend framework like React, this should look familiar.

Create a new folder in the components folder called `inputs`.

## Text Input Component

Let's generate a new component called `Text`:

```bash
php artsian make:component Text
```

This will create a file at `app/View/Text.php` and `resources/views/text.blade.php`.

Move the blade file to the `resources/views/components/inputs` folder.

You have to change the view path in the `app/View/Text.php` file:

```php
public function render()
{
    return view('components.inputs.text'); // updated path
}
```

Now add the following to the blade component:

```html
@props(['id', 'name', 'label' => null, 'type' => 'text', 'value' => '',
'placeholder' => ''])

<div class="mb-4">
  @if($label)
  <label class="block text-gray-700" for="{{ $id }}">{{ $label }}</label>
  @endif
  <input
    id="{{ $id }}"
    type="{{ $type }}"
    name="{{ $name }}"
    value="{{ old($name, $value) }}"
    class="w-full px-4 py-2 border rounded focus:outline-none @error($name) border-red-500 @enderror"
    placeholder="{{ $placeholder }}"
  />
  @error($name)
  <p class="text-red-500 text-sm mt-1">{{ $message }}</p>
  @enderror
</div>
```

This is exactly what we have in the form but it is all dynamic. We can use this component for all of our text inputs. Before we do that though, let's create components for the rest of our input types.

## Textarea Component

Let's generate a new component called `TextArea`:

```bash
php artsian make:component TextArea
```

This will create a file at `app/View/TextArea.php` and `resources/views/text-area.blade.php`.

Move the blade file to the `resources/views/components/inputs` folder.

You have to change the view path in the `app/View/TextArea.php` file:

```php
public function render()
{
    return view('components.inputs.textarea'); // updated path
}
```

Now add the following to the blade component:

```html
@props(['id', 'name', 'label' => null, 'value' => '', 'placeholder' => ''])

<div class="mb-4">
  @if($label)
  <label class="block text-gray-700" for="{{ $id }}">{{ $label }}</label>
  @endif
  <textarea
    id="{{ $id }}"
    name="{{ $name }}"
    cols="30"
    rows="7"
    class="w-full px-4 py-2 border rounded focus:outline-none @error($name) border-red-500 @enderror"
    placeholder="{{ $placeholder }}"
  >
{{ old($name, $value) }}</textarea
  >
  @error($name)
  <p class="text-red-500 text-sm mt-1">{{ $message }}</p>
  @enderror
</div>
```

## Select Component

Let's generate a new component called `select`:

```bash
php artsian make:component select
```

This will create a file at `app/View/select.php` and `resources/views/select.blade.php`.

Move the blade file to the `resources/views/components/inputs` folder.

You have to change the view path in the `app/View/select.php` file:

```php
public function render()
{
    return view('components.inputs.select'); // updated path
}
```

Now add the following to the blade component:

```html
@props(['id', 'name', 'label' => null, 'options' => [], 'value' => ''])

<div class="mb-4">
  @if($label)
  <label class="block text-gray-700" for="{{ $id }}">{{ $label }}</label>
  @endif
  <select id="{{ $id }}" name="{{ $name }}"
    class="w-full px-4 py-2 border rounded focus:outline-none @error($name) border-red-500 @enderror">
    @foreach($options as $optionValue => $optionLabel)
    <option value="{{ $optionValue }}" {{ old($name, $value)==$optionValue ? 'selected' : '' }}>
      {{ $optionLabel }}
    </option>
    @endforeach
  </select>
  @error($name)
  <p class="text-red-500 text-sm mt-1">{{ $message }}</p>
  @enderror
</div>
```

This will take in an array of options and display them as a select input.

## File Component

Let's generate a new component called `file`:

```bash
php artsian make:component file
```

This will create a file at `app/View/file.php` and `resources/views/file.blade.php`.

Move the blade file to the `resources/views/components/inputs` folder.

You have to change the view path in the `app/View/file.php` file:

```php
public function render()
{
    return view('components.inputs.file'); // updated path
}
```

Now add the following to the blade component:

```html
@props(['id', 'name', 'label' => null])

<div class="mb-4">
  @if($label)
  <label class="block text-gray-700" for="{{ $id }}">{{ $label }}</label>
  @endif
  <input
    id="{{ $id }}"
    type="file"
    name="{{ $name }}"
    class="w-full px-4 py-2 border rounded focus:outline-none @error($name) border-red-500 @enderror"
  />
  @error($name)
  <p class="text-red-500 text-sm mt-1">{{ $message }}</p>
  @enderror
</div>
```

Here is the final form with the new components:

```html
<x-layout>
  <div class="bg-white mx-auto p-8 rounded-lg shadow-md w-full md:max-w-3xl">
    <h2 class="text-4xl text-center font-bold mb-4">Create Job Listing</h2>

    <!-- Form Start -->
    <form
      method="POST"
      action="{{ route('jobs.store') }}"
      enctype="multipart/form-data"
    >
      @csrf

      <h2 class="text-2xl font-bold mb-6 text-center text-gray-500">
        Job Info
      </h2>

      <!-- Job Title -->
      <x-inputs.text
        id="title"
        name="title"
        label="Job Title"
        placeholder="Software Engineer"
      />

      <x-inputs.textarea
        id="description"
        name="description"
        label="Job Description"
        placeholder="We are seeking a skilled and motivated Software Developer..."
      />

      <x-inputs.text
        id="salary"
        name="salary"
        label="Annual Salary"
        type="number"
        placeholder="90000"
      />

      <x-inputs.textarea
        id="requirements"
        name="requirements"
        label="Requirements"
        placeholder="Bachelor's degree in Computer Science"
      />

      <x-inputs.textarea
        id="benefits"
        name="benefits"
        label="Benefits"
        placeholder="Health insurance, 401k, paid time off"
      />

      <x-inputs.text
        id="tags"
        name="tags"
        label="Tags (comma-separated)"
        type="text"
        placeholder="development,coding,java,python"
      />

      <x-inputs.select
        id="job_type"
        name="job_type"
        label="Job Type"
        :options="['Full-Time' => 'Full-Time', 'Part-Time' => 'Part-Time', 'Contract' => 'Contract', 'Temporary' => 'Temporary', 'Internship' => 'Internship', 'Volunteer' => 'Volunteer', 'On-Call' => 'On-Call']"
        value="{{ old('job_type') }}"
      />

      <x-inputs.select
        id="remote"
        name="remote"
        label="Remote"
        :options="[0 => 'No', 1 => 'Yes']"
      />

      <h2 class="text-2xl font-bold mb-6 text-center text-gray-500">
        Company Info
      </h2>

      <x-inputs.text
        id="address"
        name="address"
        label="Address"
        type="text"
        placeholder="123 Main St"
      />

      <x-inputs.text
        id="city"
        name="city"
        label="City"
        type="text"
        placeholder="Albany"
      />

      <x-inputs.text
        id="state"
        name="state"
        label="State"
        type="text"
        placeholder="NY"
      />

      <x-inputs.text
        id="zipcode"
        name="zipcode"
        label="ZIP Code"
        type="text"
        placeholder="12201"
      />

      <x-inputs.text
        id="company_name"
        name="company_name"
        label="Company Name"
        type="text"
        placeholder="Company name"
      />

      <x-inputs.textarea
        id="company_description"
        name="company_description"
        label="Company Description"
        placeholder="Company Description"
      />

      <x-inputs.text
        id="company_website"
        name="company_website"
        label="Company Website"
        type="url"
        placeholder="Enter website"
      />

      <x-inputs.text id="contact_phone" name="contact_phone" label="Contact
      Phone" type="text" " placeholder=" Enter phone" />

      <x-inputs.text
        id="contact_email"
        name="contact_email"
        label="Contact Email"
        type="email"
        placeholder="Email where you want to receive applications"
      />

      <x-inputs.file
        id="company_logo"
        name="company_logo"
        label="Company Logo"
      />

      <!-- Submit Button -->
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
