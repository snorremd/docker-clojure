# docker-clojure

This is the repository for the [official Docker image for Clojure](https://registry.hub.docker.com/_/clojure/).
It is automatically pulled and built by Stackbrew into the Docker registry.
This image runs on OpenJDK 8 and includes [Leiningen](http://leiningen.org), [boot](http://boot-clj.com) or [tools-deps](https://clojure.org/reference/deps_and_cli) (see below for tags and building instructions).

## Leiningen vs. boot vs. tools-deps

The version tags on these images look like `lein-N.N.N(-alpine)`, `boot-N.N.N(-alpine)` and `tools-deps(-alpine)`.
These refer to which version of leiningen, boot, or tools-deps is packaged in the image (because they can then install
and use any version of Clojure at runtime). The default `latest` (or `lein`, `lein-alpine`) images will always have a
recent version of leiningen installed. If you want boot, specify either `clojure:boot` / `clojure:boot-alpine` or
`clojure:boot-N.N.N` / `clojure:boot-N.N.N-alpine`. (where `N.N.N` is the version of boot you want installed). If you
want to use tools-deps, specify either `clojure:tools-deps` or `clojure:tools-deps-alpine`.

## JDK versions

Java has recently introduced a new release cadence of every 6 months and dropped the leading `1` major version number.
As of 2018-11-5, our images still default to the latest release of JDK 1.8. But we also now provide JDK 11 variants
where available (notably alpine is not yet). If you would like the JDK 11 variant, simply prefix `openjdk-11-` to the
Docker tag you use. So, for example:

JDK 1.8 tools-deps image: `clojure:tools-deps`
JDK 11 variant of that image: `clojure:openjdk-11-tools-deps`

## Alpine vs. Debian

In an effort to minimize the size of Docker images, the Docker community is migrating from traditional Linux
distributions (like Debian) to the Alpine Linux distribution. It is a very minimal distribution specifically designed
for container applications.

The traditional Debian-based Clojure images are still provided under the original tags, but you are encouraged to try
running your applications in the new `alpine` variants. Since Clojure runs on the JVM anyway, chances are everything
will just work and you'll save yourself some time and bandwidth.

## Examples

### Interactive Shell

Run an interactive shell from this image.

```
docker run -i -t clojure /bin/bash
```

Then within the shell, create a new Leiningen project and start a Clojure REPL.

```
lein new hello-world
cd hello-world
lein repl
```

### `clojure:alpine`

These images are based on the minimalist Alpine Linux distribution and are much smaller than the default (Debian-based)
images. If your app can run in them, they will be much faster to transfer and take up much less space.

## Builds

The Dockerfiles are generated by the `docker-clojure` Clojure app in this repo.

You'll need the `tools-deps` distribution of Clojure installed to run the
build. Often this just means installing the `clojure` package for your system. 

The `./build-images.sh` script will generate the Dockerfiles and build all of
the images.

## Tests

The `docker-clojure` build tool has a test suite that can be run via the
`./test.sh` script. 
