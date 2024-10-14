# Authentication & Creating Users

Now that we have full CRUD functionality, we're going to start on authentication and user registeration. Once we do that, in the next section we can start adding ownership and authorization. 

There's many ways to implement authentication in Laravel. We're going to be using the tools that are given such as the Auth facade, helper and directive, but I'll also show you how you can use Laravel Breeze to scaffold up a complete system with views and forms. We're going to go over how sessions work and the session helper. Well add the register and login forms and hook them up and we'll create a logout and show specific items in the header based on our authentication status.