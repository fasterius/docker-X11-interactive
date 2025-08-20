# `docker-X11-interactive.sh`

A helper script for starting an interactive Docker container with X11 forwarding
on MacOS. It enables graphical applications running inside the container to
display windows on the host machine, such as when you're plotting something in
an R or Python REPL.

## Features

- Runs containers ephemerally (`--rm`)
- Attaches a pseudo-TTY (`--tty`) and runs interactively (`--interactive`).
- Automatically mounts the current working directory at `/work`.
- Automatically sets the correct X11 display variable
  (`DISPLAY=docker.for.mac.host.internal:0`).
- Ensures XQuartz is running before starting the container.

## Installation

Clone this repository and place/symlink the `docker-X11-interactive.sh` script
in your `PATH`, followed by placing/symlinking the `xhost-config.sh` script into
`~/.xinitrc.d/`, for example:

```bash
git clone git@github.com:fasterius/docker-X11-interactive.git
cp docker-X11-interactive.sh ~/.local/bin/
mkdir -p ~/.xinitrc.d && cp xinitrc.d/xhost-config.sh ~/.xinitrc.d
```

## Usage

```bash
docker-X11-interactive.sh [OPTIONS] IMAGE [ARG...]
```

- `IMAGE` (required): The Docker image to run
- `OPTIONS` (optional): Extra flags to pass to docker run (_e.g._, `--gpus all`)
- `ARG...` (optional): Command to run inside the container (_e.g._, `python`)

## Examples

Run an R REPL inside a container:

```bash
docker-X11-interactive.sh rocker/tidyverse R
```

Run a Python REPL inside a container:

```bash
docker-X11-interactive.sh python:3.13 python
```
