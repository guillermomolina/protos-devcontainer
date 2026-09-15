# Protos Development Environment

A ready-to-use Dev Container for experimenting with the Protos programming language.

This repository is for **using Protos**, not for developing the Protos language implementation.

## What is included

The development environment provides:

- Protos `0.3.0`
- The official Protos VS Code extension `0.1.0`
- The supported GraalVM runtime required by the Protos `0.3.0` distribution
- A ready-to-use VS Code development environment

The bundled versions are recorded in `versions.json`.

## Getting started

Clone this repository and open it in Visual Studio Code:

```text
git clone https://github.com/guillermomolina/protos-devcontainer.git
cd protos-devcontainer
code .
```

Then reopen the folder in the Dev Container.

Once the container is ready:

```sh
protos --version
```

You should see:

```text
Protos 0.3.0
```

You can then create, edit, and run Protos programs directly inside the container.

For example:

```protos
print("Hello from Protos")
```

Save it as `hello.protos` and run:

```sh
protos hello.protos
```

You can also execute expressions directly:

```sh
protos -e 'print("Hello from Protos")'
```

## VS Code integration

The official Protos VS Code extension is installed automatically when the Dev Container is created.

It provides the Protos language integration for VS Code, including syntax highlighting and the editor functionality supported by the current extension release.

## Version policy

The exact Protos runtime version and VS Code extension version are recorded in `versions.json`.

The Protos runtime is downloaded from the corresponding GitHub release and verified using its recorded SHA-256 checksum before installation.

The VS Code extension is installed from the official Visual Studio Code Marketplace using the version recorded in `versions.json`.

The container does not use an unpinned `latest` runtime during image construction.

## Repository purpose

This repository exists to make experimenting with Protos as easy as possible:

```text
clone
  ↓
open in VS Code
  ↓
reopen in Dev Container
  ↓
write Protos
  ↓
run Protos
```

There is no need to build the Protos implementation, install Maven, or configure the Protos development toolchain.

## Developing Protos programs

This environment is intended for applications and experiments written in Protos.

The Protos compiler/runtime implementation itself is developed in the main Protos repository:

https://github.com/guillermomolina/protos

The VS Code extension is developed separately:

https://github.com/guillermomolina/protos-vscode-extension
