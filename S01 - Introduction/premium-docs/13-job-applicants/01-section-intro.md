# Job Applicants

Now it's time to add the functionality of letting users apply to jobs on the details page. We're going to use Alpine.js to create a modal that opens when we click on the apply button. The user can add fields like their name and contact info but they will also be able to upload a pdf resume.

We'll create a new migration and model for applicants. The job listing owner will see the applicants from the dashboard and will be able to download the resume and delete the applicants. We also will prevent the same user from submitting multiple applications to a single listing.