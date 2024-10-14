# Bookmark Job Listings

Now we're going to work on the bookmarking functionality. We have a button on the job details page that allows users to add the job listing to their bookmarks or saved jobs. This is so they can eaisly access it later on. There will be a link in the navigation to see all the user's bookmarks. We also want to have a remove bookmark button on the details page if the job is already bookmarked.

We're going to accolplish this by creating a new migration to create what we call a pivot table. It's purpose is to relate one resource to another. In this case users to job listings. The table will be called `user_job_bookmarks`. We'll also create a seeder to quickly add bookmarks to the test user.