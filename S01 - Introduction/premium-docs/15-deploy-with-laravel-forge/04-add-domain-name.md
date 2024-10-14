# Add Domain Name

Now that our server is setup on Forge & Digital Ocean, we need to setup the domain name. Go to the registrar of wherever you bought your domain name and add the Digital Ocean nameservers. This is so we can manage the domain via Digital Ocean.

Here are the nameservers:

- ns1.digitalocean.com
- ns2.digitalocean.com
- ns3.digitalocean.com


Now go to Digital Ocean and select "Add Domain" for your droplet. Type in the doman and select the droplet.

This will create the A record that we need. Now you just need to add a CNAME for the following:

- www: yourdomain.com

Next, we need to setup the SSL on Forge.