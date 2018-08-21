# Nginx-Craft Changelog

## 1.0.17 - 2018.08.21
### Added
* Don't allow browser caching of dynamically generated content

### Changed
* Added  "Remove if you don't plan to use server-set ENV variables" comment

## 1.0.16 - 2018.05.14
### Changed
* Removed duplicate `client_max_body_size` directives

## 1.0.15 - 2018.01.23
### Changed
* Removed incorrect `=404` directives

## 1.0.14 - 2018.01.21
### Added
* Explicitly set fastcgi_param `HTTP_HOST` to mitigate [HTTP_HOST Security Issues](https://expressionengine.com/blog/http-host-and-server-name-security-issues)
* Added `=404` as the last parameter in each of the `try_files` directives to avoid internal loops
* Added `ssi on;` to the default config for server-side includes

## 1.0.13 - 2017.12.14
### Added
* Disable limits on the maximum allowed size of the client request body via `client_max_body_size`
* Add expires headers for `mp3` files
* Updated bot UserAgents list

## 1.0.12 - 2017.11.23
### Added
* Added configuration for banning bots based on UserAgent

## 1.0.11 - 2017.10.02
### Added
* Added a `basic_localdev.com.conf` for people who just want a basic Nginx configuration for Craft local dev

## 1.0.10 - 2017.09.12
### Changed
* Updated the config to use php7.1 by default
* Added comments for the CME config

## 1.0.9 - 2017.09.01
### Changed
* Added OCSP stapling
* Tweaked TLS settings for performance
* Optimized `ssl_buffer_size` for TTFB
* Updated README.md with instructions for downloading your Issuer certificate

## 1.0.8 - 2017.08.24
### Changed
* Fixed an issue where the removal of trailing slashes could cause directory URLs to fail with "too many redirects"

## 1.0.7 - 2017.08.05
### Added
* Added `Referrer-Policy "no-referrer-when-downgrade";` to `security.conf`

## 1.0.6 - 2017.07.06
### Added
* Added handling of missing `.php` files routed through Craft
* Added `404` handler
* Added `.gitignore`

### Changed
* Removed `html` and other non-cacheable files from matching in `expires.conf`

## 1.0.5 - 2017.03.27
### Added
* Added `webp` to the `expires` header support

### Changed
* Remove `etags` from static resources
* Updated the CHANGELOG.md format

## 1.0.4 - 2017.03.02
### Added
* Added (commented out) support for error logging going to `SYSLOG` for log services
* Redirect bots probing the site for WordPress vulnerabilities
* Added information on `opcache`
* Added a redirect for Do Not Track as per https://www.eff.org/dnt-policy
* Change // -> / for all URLs, so it works for our php location block, too

### Changed
* Removed `le-well-known.conf` so that it doesn't conflict with default Forge setups
* Updated README.md

## 1.0.3 - 2016.12.10
### Added
* Added support for localized sites (commented out by default)
* Added `HTTP_PROXY`
* Added `client_max_body_size` to the README.md

### Changed
* Updated README.md

## 1.0.2 - 2016.11.30
### Added
* Added an example Forge configuration in `forge-example`
* 301 Redirect URLs with trailing /'s as per https://webmasters.googleblog.com/2010/04/to-slash-or-not-to-slash.html

### Changed
* Updated README.md

## 1.0.1 - 2016.11.09
### Added
* Added `server_tokens off` to disable sending the Nginx version number
* Added a commented out `Content-Security-Policy` header in `security.conf`

### Changed
* Updated README.md

## 1.0.0 - 2016.11.01
### Added
* Initial release

Brought to you by [nystudio107](https://nystudio107.com/)
