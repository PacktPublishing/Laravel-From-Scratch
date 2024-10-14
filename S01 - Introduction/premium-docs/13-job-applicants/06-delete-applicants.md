# Delete Applicants

Let's add the functionality to delete applicants from the job application submissions.

Open the `/resources/views/dashboard/show.blade.php` file and add the following code right under the `</p>` for the download resume button:

```html
<!-- Delete Applicant Link -->
<form
  method="POST"
  action="{{ route('applicants.destroy', $applicant->id) }}"
  onsubmit="return confirm('Are you sure you want to delete this applicant?');"
>
  @csrf @method('DELETE')
  <button type="submit" class="text-red-500 hover:text-red-700 text-sm">
    <i class="fas fa-trash-alt"></i> Delete Applicant
  </button>
</form>
```

You will get an error for now because the `destroy` method is not defined in the `ApplicantController`. Let's define it now. Start by adding the following route in the `web.php` file:

```php
Route::delete('/applicants/{applicant}', [ApplicantController::class, 'destroy'])->name('applicants.destroy')->middleware('auth');
```

Now add the method to the `ApplicantController`:

```php
// @desc   Delete a job application
// @route  DELETE /applicants/{applicant}
public function destroy($id): RedirectResponse
{
    $applicant = Applicant::findOrFail($id);
    $applicant->delete();
    return redirect()->route('dashboard.show')->with('success', 'Applicant deleted successfully.');

}
```

Now you should be able to delete applicants from the job application submissions.
