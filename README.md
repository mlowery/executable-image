# Executable Images

Note: This is only expected to work with Docker for Mac.

An executable image is an image that you run as if it were an executable.

Consider an example executable called `myexec` that prints the content of a file passed as its first argument. For this to work as a container, the path to the file inside and outside the container must match.

There is nothing novel about this project--it just captures some frequently-used `docker run` arguments that are necessary for all of this to work.

## Features Supported

* Relative paths (under any of the absolute paths below)
* `~` and `$HOME`-based paths
* `/tmp`-based paths
* Interactive apps like `vi`
* Piping to stdin and stdout

## Features Not Supported

* `$TMPDIR`-based paths: Docker for Mac automatically configures File Sharing for `/tmp` but `$TMPDIR` looks like     `/var/folders/3y/d44gn_2x7vv8d9d67969f54c0000gn/T/` which is not configured in File Sharing; the workaround is to use `/tmp` instead of `$TMPDIR`; if you pass paths based on `$TMPDIR`, they will not work; instead, use `/tmp`; example: `mktemp --tmpdir=/tmp`.

## Contents of This Project

In this project there is a helper script called `img-exec`. It is meant to capture commonly-needed arguments to `docker run` when running images as executables. You can call into it, as will be demonstrated below, or just copy-and-modify the `docker run` arguments to meet your needs.

The following files/directories are at the root of this project:

* `examples`: Discussed below.
* `img-exec`: Helper script mentioned above.
* `LICENSE-MIT.txt`: License.
* `README.md`: This file.

In the `examples` directory, there are subdirectories demonstrating different features:

* `paths`: Demonstrates passing file paths to the container.
* `pipes`: Demonstrates piping input into and out of the container.
* `vi`: Demonstrates an interactive application like `vi` (`vim`).

Each subdirectory of `examples` has the following files:

* `Dockerfile`: Used to build the Docker image for the example.
* `run`: Main script copied into the image (and used as `docker run` `--entrypoint` argument.
* `*-example`: The script that calls into the `img-exec` helper script.
* `Makefile`: Used to run `build` and `run` targets.
* `img-exec`: A symlink to the main copy of `img-exec`.
* Supporting files, if any.

To run an example, change to that directory and run `make build run`. You can look into the `Makefile`s `run` target to see how it works.

# Related

* [Executable Images - How to Dockerize Your Development Machine](https://www.infoq.com/articles/docker-executable-images)
* [bcbcarl/docker-vim](https://github.com/bcbcarl/docker-vim)
