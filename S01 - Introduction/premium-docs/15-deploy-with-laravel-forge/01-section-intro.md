# Deploy With Laravel Forge

Alright, so our application is complete, at least for now. Of ofcourse you can add to it if you want. We're going to do a full deployment and we're going to use a tool called Laravel Forge, which is in my opinion, the easiest way to bring a Laravel site to production. There is something called Laravel Cloud that is going to be released soon and it's supposebly even easier, but for now we'll use Forge along with Digital Ocean cloud hosting. 

We first need to push to Github if you haven't already. Once we setup our Forge server and Digital Ocean droplet, we're going to add a domain name. I'll be using workopia.dev but you can use your own domain. Then we'll add a free SSL certificate via Let's Encrypt. We can do this with a single click in Forge. Then we'll test everything out and we should be all set.

