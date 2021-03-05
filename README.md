# frl-online-proxy

Reverse proxy solution for Adobe customers using FRL-Online on isolated networks. In addition to a basic terminating passthrough mode, it
also supports caching, storage and forwarding.

[Read the User Guide](https://opensource.adobe.com/frl-online-proxy/)

## Getting help

All bug requests, feature requests, questions and feedback submissions are handled with Github issues. Please create a new
[issue](https://github.com/adobe/frl-online-proxy/issues) if you need any assisance or support.

## Installation

We provide automated builds for each release. These builds currently target Windows, Linux and macOS.

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

### Linux and macOS

1. Download the [latest release](https://github.com/adobe/frl-online-proxy/releases/latest). We recommend downloading it to the root of the proxy directory (e.g. `/home/[user]`)
   ```
   $ wget https://github.com/adobe/frl-online-proxy/releases/download/v1.0.1/frl-proxy-linux-1.0.1.tar.gz
   ```
2. Extract the archive
   ```
   $ tar xf frl-proxy-linux-1.0.1.tar.gz
   ```
3. The archive will extract to the directory `frl-proxy`, which contains the application binary
   ```
   $ cd frl-proxy
   $ ./frl-proxy start
   ```

## Usage

See the [User Guide](https://opensource.adobe.com/frl-online-proxy/) for details on setting up and running the FRL Online Proxy.

## Building and Running

**NOTE:** We currently provide [builds](https://github.com/adobe/frl-online-proxy/releases/latest) for Windows, Linux and macOS. If you plan to run the proxy on these platforms, we recommend installing the latest build. It is generally only necessary to build the tool if you are doing development work, need to run it on a different platform, or if your system is unable to execute the binary.

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

Any commands or options specified after the `--` will be sent to the proxy application. For example, to start the proxy in a different mode:

```
$ cargo run -- start --mode cache
```

The first time you invoke `cargo run` it will take some time to install and build all dependencies. Subsequent `cargo run` invocations will skip the build and run the binary.

### Building

Build the proxy application with `cargo build`. Once the build process completes, the `frl-proxy` binary can be found in the `target/debug` directory.

The proxy can also be built for release (which creates and optimized binary) with `cargo build --release`. This binary can be found in `target/release`.

Builds on Windows and macOS should work with just the Rust toolchain. On Linux, it may be necessary to install certain prerequisite system packages.

### Buliding on Ubuntu and other Debian variants

Ubuntu requires a few system packages to be installed in order to build the application.

```
$ sudo apt-get update
$ sudo apt install -y build-essential libssl-dev pkg-config
```

NOTE: This is known to be sufficient for Ubuntu 18.04, but should also work for Debian and other Debian variants.

### Buliding on CentOS/Redhat Enterprise Linux

CentOS/RHEL also requires some system packages before the application can be built.

```
$ sudo yum install -y gcc openssl-devel
```
