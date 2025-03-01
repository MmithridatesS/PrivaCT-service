# Project Setup Guide

This repository contains two Rust projects:
- `devnet`: A dependency service that needs to be started first.
- `ct-service`: The main service that depends on `devnet`.

## Prerequisites
Ensure you have the following installed:
- Rust (latest stable version) → [Install Rust](https://www.rust-lang.org/tools/install)
- Cargo package manager (comes with Rust)

## Building the Projects
Before running the services, you should first build both projects together using:

```sh
cargo build --workspace
```

If you encounter the following error during compilation:

```
error: `*mut ASN1_OBJECT` cannot be sent between threads safely
```

Try removing the `Cargo.lock` and `target/` directory in the affected project and then build them individually.

For `devnet`:

```sh
cd devnet
rm -f Cargo.lock
rm -rf target
cargo build
```

For `ct-service`:

```sh
cd ../ct-service
rm -f Cargo.lock
rm -rf target
cargo build
```

After successfully building the projects, proceed with running the services.

## Running the Services
### 1. Start `devnet`
First, navigate to the `devnet` directory and run the service:

```sh
cd devnet
cargo run
```

Wait until you see the following log message:

```
INFO  prism_prover::webserver > Starting webserver on 127.0.0.1:50524
```

This indicates that `devnet` is running successfully.

### 2. Start `ct-service`
Once `devnet` is running, open a new terminal and start `ct-service`:

```sh
cd ../ct-service
cargo run
```

## Configuring the Services
You can modify service configurations (such as host, port, and other settings) in the `.env` file located under `ct-service`:

```sh
cd ct-service
nano .env  # or use any text editor
```

Update the values as needed and restart the service for changes to take effect.

## Conclusion
This guide helps you set up and run the project correctly. If you run into any issues, double-check the error messages and follow the troubleshooting steps above.

Additionally, after starting the services, let them run for **around 10 minutes** to ensure that the accounts in `devnet` containing the STH of `ct-log` get properly updated.
