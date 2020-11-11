# frl-proxy

Reverse proxy solution for customers using FRL-Online on isolated networks.

## Usage

```
frl-proxy 0.4.0
FRL Proxy

USAGE:
    frl-proxy.exe <SUBCOMMAND>

FLAGS:
    -h, --help       Prints help information
    -V, --version    Prints version information

SUBCOMMANDS:
    help           Prints this message or the help of the given subcommand(s)
    init-config    Create a template config file
    start          Start the proxy server
```

### `start`

Start the proxy. By default, it will run a plain HTTP server listening on `127.0.0.1:3030`, forwarding to `https://lcs-cops.adobe.io`.

```
frl-proxy.exe-start 0.4.0
Start the proxy server

USAGE:
    frl-proxy.exe start [FLAGS] [OPTIONS]

FLAGS:
    -h, --help       Prints help information
        --ssl
    -V, --version    Prints version information

OPTIONS:
    -c, --config-file <config-file>
        --host <host>
        --remote-host <remote-host>
        --ssl-cert <ssl-cert>
        --ssl-key <ssl-key>
```

### `init-config`

Initialize a config file template. The config file is optional. It is used to define proxy defaults (host, remote host, ssl settings) and to
override logging defaults.

The `-o/--out-file` option defines the path to the new config file. By default, the file will be named `config.toml` and be placed in the
current working directory.

```
frl-proxy.exe-init-config 0.4.0
Create a template config file

USAGE:
    frl-proxy.exe init-config [OPTIONS]

FLAGS:
    -h, --help       Prints help information
    -V, --version    Prints version information

OPTIONS:
    -o, --out-file <out-file>     [default: config.toml]
```

## Building and Running

To build the proxy application, make sure you have the [Rust toolchain](https://rustup.rs/) installed on your system.

Then, from a terminal, clone this project.

```
$ git clone git@git.corp.adobe.com:dmeservices/frl-proxy.git
$ cd frl-proxy
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
