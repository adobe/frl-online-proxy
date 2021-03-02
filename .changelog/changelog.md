| tag | date | title |
|---|---|---|
| v1.0.0 | 2021-02-25 | frl-online-proxy v1.0.0 |

### Added
* Cache functionality with store and forward modes ([#4])
    * New commands for cache control ([#8], [#10]):
        * `clear` to clear the cache with confirmation
        * `export` to export requests to an external forwarder
        * `import` to import responses from an external forwarder
* Guided wizard for creating config files ([#14])
    * command-line flags for overriding configuration file options:
        * `-d` global option to force debug log level
        * `-l` global option to choose log destination (console or file)
        * `--mode` option on `start` command to choose cache mode
        * `--ssl` option on `start` command to enable/disable SSL
    * environment variables can be used for sensitive configuration data (such as certificate password)

### Changed
* added/updated package dependencies ([#4], [#17])
    * latest tokio for general async support
    * native-tls rather than rustls for SSL support
        * certificates in `pkcs` rather than `pem` format
    * latest sqlx for async sqlite support
* use of config file is now required ([#11])

### Fixed
* database updates are now transactional ([#17])
* database files are explicitly closed at end of each run ([#17])

[#4]: https://github.com/adobe/frl-online-proxy/pull/4
[#8]: https://github.com/adobe/frl-online-proxy/pull/8
[#10]: https://github.com/adobe/frl-online-proxy/pull/10
[#11]: https://github.com/adobe/frl-online-proxy/pull/11
[#14]: https://github.com/adobe/frl-online-proxy/pull/14
[#17]: https://github.com/adobe/frl-online-proxy/pull/17

---

| tag | date | title |
|---|---|---|
| v0.5.1 | 2021-01-05 | frl-online-proxy v0.5.1 |

Improved error handling for invalid SSL key.

---

| tag | date | title |
|---|---|---|
| v0.5.0 | 2020-11-12 | frl-online-proxy v0.5.0 |

First release of the Adobe FRL Online Proxy. 

Feature Summary:

* Live proxy mode (offline caching is planned for a future release)
* SSL Support
* Service management tools for Windows
