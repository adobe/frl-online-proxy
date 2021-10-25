# New Features

\#25 Upstream Proxy Support

To use the new capabilities, run the `configure` command to reconfigure your proxy.  Accept all your existing settings until you get to the new question `Does your network require this proxy to use an upstream proxy?`. Answer Yes (y) and you will be prompted to enter the proxy host and port of your upstream proxy (only http proxies are currently supported).  Then you will be asked if your proxy requires authentication (only basic authentication is currently supported) and, if you say yes, you will be prompted for a username and password.  At that point, you are all set: all requests from the FRL proxy will be directed through the upstream proxy.

As to timeouts: the FRL proxy would never timeout before, but the application clients would, so there was no visible effect of this failure to timeout unless you ran the proxy for an incredibly long time (at which point its memory usage would rise).  The FRL proxy now has a 59 second timeout on all upstream calls, which is just under the client timeout of 60 seconds.  It gives a 502 response to the client, which will cause the client to retry its request once.
