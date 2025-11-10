# SOME/IP Communication Demo

This repository contains a small demo of inter-process communication using vSomeIP (Scalable service-Oriented MiddlewarE over IP). It was created during an internship to demonstrate service discovery, subscription, notifications and request/response interactions in an automotive middleware context.

## Prerequisites

- CMake (3.10+ recommended)
- A C/C++ toolchain (make/gcc on Linux, Visual Studio on Windows, etc.)
- vSomeIP library (vSomeIP) and headers
- Optional: a POSIX-like shell for Linux/macOS instructions;

## Build

Recommended: build in a separate directory.

### Linux / macOS (Bash)

```bash
mkdir -p build && cd build
cmake ..
make
```

## Run

The demo uses JSON configuration files (for example: `server.json`, `client1.json`, `client2.json`) and environment variables to choose which configuration to load. Run the three processes in separate terminals.

### Bash example (Linux / macOS)

```bash
# Terminal 1 (server)
export VSOMEIP_CONFIGURATION=server.json
export VSOMEIP_APPLICATION_NAME=service-app
./bin/server_main

# Terminal 2 (client1)
export VSOMEIP_CONFIGURATION=client1.json
export VSOMEIP_APPLICATION_NAME=client1-app
./bin/client1_main

# Terminal 3 (client2)
export VSOMEIP_CONFIGURATION=client2.json
export VSOMEIP_APPLICATION_NAME=client2-app
./bin/client2_main
```

## Configuration

The demo reads vSomeIP configuration from JSON files. Examples include connection, service and notification settings. Edit `server.json`, `client1.json`, and `client2.json` to adapt addresses, ports, or service IDs.

## Logging & Debugging

- vSomeIP outputs logs to stdout/stderr — review console output for service discovery and message traces.
- If network discovery fails, ensure the hosts are on the same network/subnet and the JSON configuration matches.

## Notes

- This project uses vSomeIP. Make sure the library and headers are available when building.
- The run examples assume the `bin/` folder contains the built executables.
