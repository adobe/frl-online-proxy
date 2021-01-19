# frl-online-proxy

Reverse proxy solution for Adobe customers using FRL-Online on isolated networks. In addition to a basic terminating passthrough mode, it
also supports caching, storage and forwarding.

[Read the User Guide](https://opensource.adobe.com/frl-online-proxy/)

## Getting help

All bug requests, feature requests, questions and feedback submissions are handled with Github issues. Please create a new
[issue](https://github.com/adobe/frl-online-proxy/issues) if you need any assisance or support.

## Installation

We provide automated builds for each release. These builds currently target Windows and Linux.

### Windows

1. Download the [latest release](https://github.com/adobe/frl-online-proxy/releases/latest).
2. Open the application zip
3. Copy the `frl-proxy` directory to your desired root location
4. Open a PowerShell terminal
5. Change directory to the frl-proxy location
   ```
   > cd c:\path\to\frl-proxy
   ```
6. Run the proxy
   ```
   > .\frl-proxy.exe start
   ```

### Linux

1. Download the [latest release](https://github.com/adobe/frl-online-proxy/releases/latest). We recommend downloading it to the root of the proxy directory (e.g. `/home/[user]`)
   ```
   $ wget https://github.com/adobe/frl-online-proxy/releases/download/v0.5.1/frl-proxy-linux-0.5.1.tar.gz
   ```
2. Extract the archive
   ```
   $ tar xf frl-proxy-linux-0.5.1.tar.gz
   ```
3. The archive will extract to the directory `frl-proxy`, which contains the application binary
   ```
   $ cd frl-proxy
   $ ./frl-proxy start
   ```

## Usage

```
frl-proxy 0.9.0
FRL Proxy

USAGE:
    frl-proxy.exe <SUBCOMMAND>

FLAGS:
    -h, --help       Prints help information
    -V, --version    Prints version information

SUBCOMMANDS:
    cache-control    Manage the cache file
    help             Prints this message or the help of the given subcommand(s)
    init-config      Create a template config file
    start            Start the proxy server
```

### `start`

Start the proxy. By default, it will run a plain HTTP server listening on `127.0.0.1:3030`, forwarding to `https://lcs-cops.adobe.io`.
The default mode of operation is `passthrough` which means that caching is disabled.

```
frl-proxy.exe-start 0.9.0
Start the proxy server

USAGE:
    frl-proxy.exe start [OPTIONS]

FLAGS:
    -h, --help       Prints help information
    -V, --version    Prints version information

OPTIONS:
    -c, --config-file <config-file>      Path to optional config file
        --host <host>                    Proxy hostname
    -m, --mode <mode>                    Mode to run the proxy in, one of passthrough, cache, store, or forward. You can
                                         use any prefix of these names (minimally p, c, s, or f)
        --remote-host <remote-host>      Remote (licensing server) hostname
        --ssl <ssl>                      Enable SSL? (true or false)
        --ssl-cert <ssl-cert>            Path to SSL certificate (pkcs12 format)
        --ssl-password <ssl-password>    SSL certificate password
```

### `init-config`

Initialize a config file template. The config file is optional. It is used to define proxy defaults (host, remote host, ssl settings) and to
override logging defaults.

The `-o/--out-file` option defines the path to the new config file. By default, the file will be named `config.toml` and be placed in the
current working directory.

```
frl-proxy.exe-init-config 0.9.0
Create a template config file

USAGE:
    frl-proxy.exe init-config [OPTIONS]

FLAGS:
    -h, --help       Prints help information
    -V, --version    Prints version information

OPTIONS:
    -o, --out-file <out-file>    path to config filename [default: config.toml]
```

### `cache-control`

Options for managing cache database. Currently supports clearing the cache. Import and export are coming soon.

```
frl-proxy.exe-cache-control 0.9.0
Manage the cache file

USAGE:
    frl-proxy.exe cache-control [FLAGS] [OPTIONS]

FLAGS:
        --clear      Whether to clear the cache (dangerous!)
    -h, --help       Prints help information
    -V, --version    Prints version information
    -y               Bypass confirmation prompts

OPTIONS:
    -C, --cache-file <cache-file>      Path to cache file
    -c, --config-file <config-file>    Path to optional config file
    -e, --export-file <export-file>    Export cache to a file (not yet implemented)
    -i, --import-file <import-file>    Import cache from a file (not yet implemented)
```

## Building and Running

**NOTE:** We currently provide [builds](https://github.com/adobe/frl-online-proxy/releases/latest) for Windows and Linux. If you plan to run the proxy on these platforms, we recommend installing the latest build. It is generally only necessary to build the tool if you are doing development work, need to run it on a different platform, or if your system is unable to execute the binary.

To build the proxy application, make sure you have the [Rust toolchain](https://rustup.rs/) installed on your system.

Then, from a terminal, clone this project.

```
$ git clone https://github.com/adobe/frl-online-proxy.git
$ cd frl-online-proxy
```

### Running with Cargo

To run the proxy application, invoke `cargo run`. This installs dependencies, compiles, links, assembles and runs the executable.

```
$ cargo run -- start
```

Any commands or options specified after the `--` will be sent to the proxy application. For example, to start the proxy with a different host:

```
$ cargo run -- start --host 0.0.0.0:8080
```

The first time you invoke `cargo run` it will take some time to install and build all dependencies. Subsequent `cargo run` invocations will skip the build and run the binary.

### Building

Build the proxy application with `cargo build`. Once the build process completes, the `frl-proxy` binary can be found in the `target/debug` directory.

The proxy can also be built for release (which creates and optimized binary) with `cargo build --release`. This binary can be found in `target/release`.

### Buliding on Ubuntu

Ubuntu requires a few system packages to be installed in order to build the application.

```
$ sudo apt-get update
$ sudo apt install -y build-essential libssl-dev pkg-config
```

NOTE: This is known to be sufficient for Ubuntu 18.04, but should also work for Debian and other Debian variants.

### Buliding on CentOS

CentOS/RHEL also requires some system packages before the application can be built.

```
$ sudo yum install -y gcc openssl-devel
```
