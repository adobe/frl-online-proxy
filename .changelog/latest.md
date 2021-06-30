The docs are not ready yet, but we have upstream proxy and timeout support working so we are doing a pre-release to allow for general beta testing.

To use the new capabilities, run the `configure` command to reconfigure your proxy.  Accept all your existing settings until you get to the new question `Does your network require this proxy to use an upstream proxy?`. Answer Yes (y) and you will be prompted to enter the proxy host and port of your upstream proxy (only http proxies are currently supported).  Then you will be asked if your proxy requires authentication (only basic authentication is currently supported) and, if you say yes, you will be prompted for a username and password.  At that point, you are all set: all requests from the FRL proxy will be directed through the upstream proxy.

As to timeouts: the FRL proxy would never timeout before, but the application clients would, so there was no visible effect of this failure to timeout unless you ran the proxy for an incredibly long time (at which point its memory usage would rise).  The FRL proxy now has a 59 second timeout on all upstream calls, which is just under the client timeout of 60 seconds.  It gives a 502 response to the client, which will cause the client to retry its request once.

### Added
* The ability to use an upstream proxy ([#25])
    * Extend the `configure` command to collect proxy info.
    * Redirect all upstream requests through a configured proxy.
    * Support use of basic authentication if required.
    * NOTE: Only http proxies are supported at this time.
    
### Fixed
* Put a 59 second timeout limit on upstream calls [#27]
    * Return a 502 (Gateway failure) response to client on timeout.
