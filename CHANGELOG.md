# Nginx-Craft Changelog

## 1.0.7 - 2017.08.05
### Added
* Added `Referrer-Policy "strict-origin-when-cross-origin";` to `security.conf`

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
