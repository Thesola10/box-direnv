# box-direnv

A wrapper around `distrobox` or `toolbox` to provide commands which exist in a dev container, in the host environment transparently.

Heavily inspired by [nix-direnv].

## Installation

Put the following lines in your `.envrc`:

```bash
if ! has box_direnv_version || ! box_direnv_version 0.1.1; then
  source_url "https://raw.githubusercontent.com/thesola10/box-direnv/0.1.1/direnvrc" "sha256-CsiXN7IanSkdwPX5Ejr7pUkrIMbK93hsBoLzsP9YdLs="
fi
```

## Usage example

`box-direnv` supports a few scenarios, depending on the parameters given:

### Distrobox's `distrobox.ini` (recommended)

Create a [`distrobox.ini`] file in your project root, which will describe the Distrobox container providing your environment, then add the line `use distrobox`:

```console
$ echo "use distrobox" >> .envrc
$ direnv allow
```

Optionally, you can specify a box name:

```console
$ echo "use distrobox my_box" >> .envrc
$ direnv allow
```

### From image registry

Add the line `use distrobox <image>` or `use toolbox <image>` to tell box-direnv to create a container from that image. For example:

```console
$ echo "use distrobox registry.fedoraproject.org/fedora-toolbox"
$ direnv allow
```

### From local `Dockerfile`/`Containerfile`

You may wish to customize your container image before entering the environment. In this case, you can tell box-direnv to use a local build context directly.

Add the line `use distrobox <path to Containerfile>` or `use toolbox <path to Containerfile>` to tell box-direnv to build an image from that directory, then use it to create the container. For example:

```console
$ echo "use toolbox ./docker"
$ direnv allow
```

[nix-direnv]: https://github.com/nix-community/nix-direnv
[`distrobox.ini`]: https://github.com/89luca89/distrobox/blob/main/docs/usage/distrobox-assemble.md
