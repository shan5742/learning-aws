I have a personal site which hosts this blog over at [asamshan.dev](https:www.asamshan.dev). It is currently hosted by Netlify, which works great and is totally free, which is awesome, but it handles everything for you seamlessly. Given that I have been working on more operations stuff, I figured I should host my site on an aws instance.

### Getting Setup

First up I needed to enable AWS's _Route 53_. I created a hosted public server and added various DNS records (A and CNAME). Next up I had to repoint my domain from Netlify's DNS to the AWS ones I just created. Easy enough so far.

### Moving My Site to VPS Instance

I created a fresh build of my site via **Gatsby**, just a simple `gatsby build` command. Now I needed to get this folder over to my instance. For this I am using **SCP**, this can be done with one command from my local machine:

```
scp -i <path-to-ssh-key> <directory-to-transfer> ubuntu@<vps-ip>:~<location-on-vps>
```

I put this on the root of my VPS just to keep things simple, a better place would have been to dump it straight into the correct NGINX directory, but at the time I hadn't setup my web server so this wasn't an option. So next up was installing and configuring NGINX

### NGINX Setup

First I needed to install NGINX on VPS

```
sudo apt update
sudo apt install nginx
```

To check everything was working I simply pointed my browser to my VPS IP and viola the default Nginx page appeared. Now I just needed to modify my VPS security group to open up port 80 (default port for NGINX).

### Tweaking NGINX to serve my site

First I needed to move the files transferred from my local machine to `/var/www/main` I chose to call it main as it is going to be the main site that my web server is hosting.

From there I needed to update the document root `/etc/nginx/sites-enabled/default` to point to the newly created main directory and that is it in terms of serving the site for now.

Anybody pinging my VPS IP would get my site - great - but I want people to hitm y domain and get the site right.

### First up https

I wanted my site to be served over https, until now Netlify would handle this for me, so to host on my VPS I would need my own certificate. Luckily there is a great tool for this - [certbot](https://certbot.eff.org/lets-encrypt/ubuntubionic-nginx).

I simpley ssh into my vps as normal and install certbot via snap with the following command:

```
sudo snap install --classic certbot
```

Certbot has a cool cli that handles all the nginx config for you:

```
sudo certbot --nginx
```

### Job Done?

Almost... the above gets <asamshan.dev> working, but if someone was to point their browser to <www.asamshan.dev> the site would not be served. What's the fix? Well I need to go back to nginx config and modify to handle all sub-domains.
