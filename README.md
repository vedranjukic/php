## Summary

*Develop PHP based applications. Includes needed tools, extensions, and dependencies.*

| Metadata | Value |  
|----------|-------|
| *Categories* | Languages |
| *Image type* | Dockerfile |
| *Published images* | mcr.microsoft.com/devcontainers/php |
| *Available image variants* | 8 / 8-bullseye, 8.1 / 8.1-bullseye, 8.0 / 8.0-bullseye, 7 / 7-bullseye, 7.4 / 7.4-bullseye, 8-buster, 8.1-buster, 8.0-buster, 7-buster, 7.5-buster ([full list](https://mcr.microsoft.com/v2/devcontainers/php/tags/list)) |
| *Published image architecture(s)* | x86-64, arm64/aarch64 for `bullseye` variants |
| *Container host OS support* | Linux, macOS, Windows |
| *Container OS* | Debian |
| *Languages, platforms* | PHP |

## Using this image

You can directly reference pre-built versions of `Dockerfile` by using the `image` property in `.devcontainer/devcontainer.json` or updating the `FROM` statement in your own `Dockerfile` with one of the following:

- `mcr.microsoft.com/devcontainers/php` (latest)
- `mcr.microsoft.com/devcontainers/php:8` (or `8-bullseye`, `8-buster` to pin to an OS version)
- `mcr.microsoft.com/devcontainers/php:8.1` (or `8.1-bullseye`, `8.1-buster` to pin to an OS version)
- `mcr.microsoft.com/devcontainers/php:8.0` (or `8.0-bullseye`, `8.0-buster` to pin to an OS version)
- `mcr.microsoft.com/devcontainers/php:7` (or `7-bullseye`, `7-buster` to pin to an OS version)
- `mcr.microsoft.com/devcontainers/php:7.4` (or `7.4-bullseye`, `7.4-buster` to pin to an OS version)

You can decide how often you want updates by referencing a [semantic version](https://semver.org/) of each image. For example:

- `mcr.microsoft.com/devcontainers/python:0-7` (or `0-7-bullseye`, `0-7-buster`)
- `mcr.microsoft.com/devcontainers/python:0.203-7` (or `0.203-7-bullseye`, `0.203-7-buster`)
- `mcr.microsoft.com/devcontainers/python:0.203.3-7` (or `0.203.3-7-bullseye`, `0.203.3-7-buster`)

However, security patching is done only on the latest non-breaking, in support versions of images. You may want to run `apt-get update && apt-get upgrade` in your Dockerfile if you lock to a more specific version to at least pick up OS security updates.

Alternatively, you can use the contents of `Dockerfile` to fully customize your container's contents or to build it for a container host architecture not supported by the image.

### Installing Node.js

Given JavaScript front-end web client code written for use in conjunction with a PHP back-end often requires the use of Node.js-based utilities to build, this container also includes `nvm` so that you can easily install Node.js. 

Also, you can use a Node feature to install any version of Node by adding the following to `devcontainer.json`:

```json
{
  "features": {
    "ghcr.io/devcontainers/features/node:1": {
      "version": "latest"
    }
  }
}
```

### Starting / stopping Apache

This dev container includes Apache in addition to the PHP CLI. While you can use PHP's built in CLI (e.g. `php -S 0.0.0.0:8080`), you can start Apache by running:

```bash
apache2ctl start
```

Apache will be available on port `8080`.

If you want to wire in something directly from your source code into the `www` folder, you can add a symlink as follows to `postCreateCommand`:

```json
"postCreateCommand": "sudo chmod a+x \"$(pwd)\" && sudo rm -rf /var/www/html && sudo ln -s \"$(pwd)\" /var/www/html"
```

...or execute this from a terminal window once the container is up:

```bash
sudo chmod a+x "$(pwd)" && sudo rm -rf /var/www/html && sudo ln -s "$(pwd)" /var/www/html
```