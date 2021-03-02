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
