# Executable Images

Note: This is only expected to work with Docker for Mac.

An executable image is an image that you run as if it were an executable. It is not interactive.

Consider an example executable called `myexec` that prints the content of a file passed as its first argument. For this to work as a container, the path to the file inside and outside the container must match. This can be accomplished via volumes. There is nothing novel here--I'm just documenting some frequently-used `docker` arguments that are necessary for this to work.

## Paths Supported

* Relative paths (under any of the absolute paths below)
* `~` and `$HOME`-based paths
* `/tmp`-based paths

## Contents of This Project

In this project there is a helper script called `img-exec`. It is meant to capture commonly-needed arguments to `docker` when running images as executables. You can call into it, as will be demonstrated below, or just copy-and-modify it to meet your needs.

In the `example` directory, there is a script called `myexec` that calls into `img-exec`. There is also a `hello.txt` file that is a sample input to `myexec`.

In the `example/img` directory, there is a `Dockerfile` which simply bundles the "real" `myexec` executable into an image.

## Running the Example

The following commands assume you've cloned this project to `~/executable-image`.

1. Build the image:

    ```console
    $ cd ~/executable-image/example/img
    $ docker build -t myexecimg .
    ```
1. Add `myexec` and `img-exec` script directories to your `PATH`:

    ```console
    $ cd ~/executable-image
    $ export PATH=$(pwd):$PATH
    $ cd ~/executable-image/example
    $ export PATH=$(pwd):$PATH
    ```

1. Then call `myexec` with arguments. The first one is a relative path:

    ```console
    $ cd ~/executable-image/example
    $ myexec hello.txt
    Hello world!
    ```

1. The next one uses `~`:

    ```console
    $ myexec ~/executable-image/example/hello.txt
    Hello world!
    ```

1. The last one uses `/tmp` (`hello.txt` is first copied to `/tmp`):

    ```console
    $ cp ~/executable-image/example/hello.txt /tmp
    $ myexec /tmp/hello.txt
    Hello world!
    ```

# Related

* [Executable Images - How to Dockerize Your Development Machine](https://www.infoq.com/articles/docker-executable-images)