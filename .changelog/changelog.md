| tag | date | title |
|---|---|---|
| v1.1.0 | 2021-10-25 | frl-online-proxy v1.1.0 |

# New Features

\#25 Upstream Proxy Support

To use the new capabilities, run the `configure` command to reconfigure your proxy.  Accept all your existing settings until you get to the new question `Does your network require this proxy to use an upstream proxy?`. Answer Yes (y) and you will be prompted to enter the proxy host and port of your upstream proxy (only http proxies are currently supported).  Then you will be asked if your proxy requires authentication (only basic authentication is currently supported) and, if you say yes, you will be prompted for a username and password.  At that point, you are all set: all requests from the FRL proxy will be directed through the upstream proxy.

As to timeouts: the FRL proxy would never timeout before, but the application clients would, so there was no visible effect of this failure to timeout unless you ran the proxy for an incredibly long time (at which point its memory usage would rise).  The FRL proxy now has a 59 second timeout on all upstream calls, which is just under the client timeout of 60 seconds.  It gives a 502 response to the client, which will cause the client to retry its request once.

---

| tag | date | title |
|---|---|---|
| v1.0.1 | 2021-02-25 | frl-online-proxy v1.0.0 |

**NOTE:** The only new addition for this release is the macOS build, so we are re-posting the notes for the
last release.

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
