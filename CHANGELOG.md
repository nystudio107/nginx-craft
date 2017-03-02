# Nginx-Craft Changelog

## 1.0.4 - 2017.03.02

* [Added] Added (commented out) support for error logging going to `SYSLOG` for log services
* [Added] Redirect bots probing the site for WordPress vulnerabilities
* [Added] Added information on `opcache`
* [Improved] Removed `le-well-known.conf` so that it doesn't conflict with default Forge setups
* [Added] Added a redirect for Do Not Track as per https://www.eff.org/dnt-policy
* [Added] Change // -> / for all URLs, so it works for our php location block, too
* [Improved] Updated README.md

## 1.0.3 - 2016.12.10

* [Added] Added support for localized sites (commented out by default)
* [Added] Added `HTTP_PROXY`
* [Added] Added `client_max_body_size` to the README.md
* [Improved] Updated README.md

## 1.0.2 - 2016.11.30

* [Added] Added an example Forge configuration in `forge-example`
* [Added] 301 Redirect URLs with trailing /'s as per https://webmasters.googleblog.com/2010/04/to-slash-or-not-to-slash.html
* [Improved] Updated README.md

## 1.0.1 - 2016.11.09

* [Added] Added `server_tokens off` to disable sending the Nginx version number
* [Added] Added a commented out `Content-Security-Policy` header in `security.conf`
* [Improved] Updated README.md

## 1.0.0 - 2016.11.01

* [Added] Initial release

Brought to you by [nystudio107](https://nystudio107.com/)
