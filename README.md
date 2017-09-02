# nginx-craft

An Nginx virtual host configuration for Craft CMS that implements a number of best-practices.

## Overview

### What it handles

The Nginx-Craft configuration handles:

* Redirecting from HTTP to HTTPS
* Canonical domain rewrites from www.SOMEDOMAIN.com to SOMEDOMAIN.com
* 301 Redirect URLs with trailing /'s as per https://webmasters.googleblog.com/2010/04/to-slash-or-not-to-slash.html
* Setting `PATH_INFO` properly via php-fpm -> PHP
* "Far-future" Expires headers
* Adding XSS and other security headers
* Gzip compression
* Filename-based cache busting for static resources
* IPv4 and IPv6 support
* http2 support
* Reasonable SSL cipher suites and TLS protocols
* Localized sites

### Assumptions made

The following are assumptions made in this configuration:

* The site is https
* The SSL certificate is from LetsEncrypt.com
* The canonical domain is SOMEDOMAIN.com (no www.)
* Nginx is version 1.9.5 or later (and thus supports http2)
* Paths are standard Ubuntu, change as needed
* You're using php7 via php-fpm
* You have `'omitScriptNameInUrls' => true,` in your `craft/general.php`

If any of these assumptions are invalid, make the appropriate changes.

### What's included

This Nginx configuration comes in two parts:

* `sites-available/somedomain.com.conf` - an Nginx virtual host configuration file tailored for Craft CMS; it will require some minor customization for your domain
* `nginx-partials` - some Nginx configuration partials used by all of the virtual hosts, logically segregated.  These don't need to be changed, but can be selectively disabled by changing the suffix to `.off` (or anything other than `.conf`)

## Using Nginx-Craft

1. Obtain an SSL certificate for your domain via [LetsEncrypt.com](https://letsencrypt.org/) (or via other certificate authorities).  LetsEncrypt.com is free, and it's automated.  You will need a basic server up and running that responds to port 80 to do this, [LetsEnecrypt/Nginx tutorial](https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-ubuntu-16-04)
2. Create a `dhparam.pem` via `sudo openssl dhparam -out /etc/ssl/certs/dhparam.pem 2048`
3. Download your Issuer certificate via `sudo wget -O /etc/nginx/certs/lets-encrypt-x3-cross-signed.pem "https://letsencrypt.org/certs/lets-encrypt-x3-cross-signed.pem"`
4. Upload the entire `nginx-partials` folder to `/etc/nginx/`
5. Rename the `somedomain.com.conf` file to `yourdomain.com.conf`
6. Do a search & replace in `yourdomain.com.conf` to change `SOMEDOMAIN` -> `yourdomain`
7. Tweak any paths that may need changing on your server
8. Restart nginx via `sudo nginx -s reload`

If you're using [Forge](https://forge.laravel.com/), it takes care of a number of these things for you, but still needs tuning.  Use the `somedomain.com.conf` file as a guide, making sure to not change any of the directives labeled `# FORGE CONFIG (DOT NOT REMOVE!)` in your existing `.conf` file.

The same applies for CloudWays, ServerPilot, Homestead, MAMP, etc.

For further information on TLS optimization, see the [How to properly configure your nginx for TLS](https://medium.com/@mvuksano/how-to-properly-configure-your-nginx-for-tls-564651438fe0) article.

## Forge & opcache

**N.B.:** Forge now has `opcache` functionality baked-in, you can enable it via the Server settings, so this information is largely deprecated.

If you're using Forge, understand that `opcache` is off by default. To enable it, go to your server in Forge, click on *Edit Files* and choose *Edit PHP FPM Configuration* and search on `opcache`. Here are the defaults I use; tweak them to suit your needs:

    [opcache]
    ; Determines if Zend OPCache is enabled
    opcache.enable=1

    ; Determines if Zend OPCache is enabled for the CLI version of PHP
    ;opcache.enable_cli=0

    ; The OPcache shared memory storage size.
    opcache.memory_consumption=256

    ; The amount of memory for interned strings in Mbytes.
    opcache.interned_strings_buffer=16

    ; The maximum number of keys (scripts) in the OPcache hash table.
    ; Only numbers between 200 and 100000 are allowed.
    opcache.max_accelerated_files=8000

    ; If disabled, all PHPDoc comments are dropped from the code to reduce the
    ; size of the optimized code.
    opcache.save_comments=0

More about tweaking `opcache` can be found in the [Fine-Tune Your Opcache Configuration to Avoid Caching Suprises](https://tideways.io/profiler/blog/fine-tune-your-opcache-configuration-to-avoid-caching-suprises) article. The [Best Zend OpCache Settings/Tuning/Config](https://www.scalingphpbook.com/blog/2014/02/14/best-zend-opcache-settings.html) article is very useful as well.

## Miscellanea

If you encounter a problem where large asset uploads fail, despite `memory_limit`, `post_max_size` and `upload_max_filesize` being set properly in your `php.ini`, you may need to add the following to the `http {}` block of the main `nginx.conf`:

    client_max_body_size 20M;

Brought to you by [nystudio107](https://nystudio107.com/)
