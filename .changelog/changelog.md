v0.9.0

Feature summary:

* First release of cache, store and forward funtionality
* `--mode` option
  * `passthrough` - do not cache, make live calls only \[default\]
  * `cache` - cache request/response data and also make live calls to licensing service (if available)
  * `store` - cache, but do not make live calls
  * `forward` - execute all licensing activation and deactivation requests with licensing service and cache response data
* `cache-control` command - manage the cache database
  * `--clear` - clear a cache database
* `cache.cache_file_path` added to config file to specify cache DB file path
  * Can be overridden from command-line with `-C/--config-file`
* SSL cert now authenticated with password instead of key

---

v0.5.1 - 2021-01-05

Improved error handling for invalid SSL key.

---

First release of the Adobe FRL Online Proxy. 

Feature Summary:

* Live proxy mode (offline caching is planned for a future release)
* SSL Support
* Service management tools for Windows

v0.5.0 - 2020-11-12
