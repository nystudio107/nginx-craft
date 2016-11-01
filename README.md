# nginx-craft

An Nginx virtual host configuration for Craft CMS that implements a number of best-practices.

## Overview

### What it handles

The Nginx-Craft configuration handles:

* Redirecting from HTTP to HTTPS
* Canonical domain rewrites from www.SOMEDOMAIN.com to SOMEDOMAIN.com
* Setting `PATH_INFO` properly via php-fpm -> PHP
* "Far-future" Expires headers
* Adding XSS and other security headers
* Gzip compression
* Filename-based cache busting for static resources
* IPv4 and IPv6 support
* http2 support
* Reasonable SSL cipher suites and TLS protocols

### Assumptions made

The following are assumptions made in this configuration:

* The site is https
* The SSL certificate is from LetsEncrypt.com
* The canonical domain is SOMEDOMAIN.com (no www.)
* Nginx is version 1.9.5 or later (and thus supports http2)
* Paths are standard Ubuntu, change as needed

If any of these assumptions are invalid, make the appropriate changes.

### What's included

This Nginx configuration comes in two parts:

* `sites-available/somedomain.com.conf` - an Nginx virtual host configuration file tailored for Craft CMS; it will require some minor customization for your domain
* `nginx-partials` - some Nginx configuration partials used by all of the virtual hosts, logically segregated.  These don't need to be changed, but can be selectively disabled by changing the suffix to `.off` (or anything other than `.conf`)

## Using Nginx-Craft

1. Obtain an SSL certificate for your domain via [LetsEncrypt.com](https://letsencrypt.org/) (or via other certificate authorities).  LetsEncrypt.com is free, and it's automated.  You will need a basic server up and running that responds to port 80 to do this, [LetsEnecrypt/Nginx tutorial](https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-ubuntu-16-04)
2. Create a `dhparam.pem` via `sudo openssl dhparam -out /etc/ssl/certs/dhparam.pem 2048`
3. Upload the entire `nginx-partials` folder to `/etc/nginx/`
4. Rename the `somedomain.com.conf` file to `yourdomain.com.conf`
5. Do a search & replace in `yourdomain.com.conf` to change `SOMEDOMAIN` -> `yourdomain`
6. Tweak any paths that may need changing on your server
7. Restart nginx via `sudo nginx -s reload`

If you're using [Forge](https://forge.laravel.com/), use the above file as a guide, making sure to not change any of the directives labeled `# FORGE CONFIG (DOT NOT REMOVE!)` in your existing `.conf` file.

## Nginx-Craft Changelog

### 1.0.0 -- 2016.11.01

* Initial release

Brought to you by [nystudio107](https://nystudio107.com/)
