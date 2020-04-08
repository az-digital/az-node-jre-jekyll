# Node.js and Java environment with the Jekyll static web site builder

The base is a stable version of the official Node.js, with the Jekyll static
web site builder added into this from a full Ruby development environment
(through a multi-stage build defined in the Dockerfile), but leaving the Ruby
development tools behind. The official AWS command-line tools defined as a
Python package are also in the image, but the installation for these uses
binary (Wheel) packages, so does not require a full Python development
environment. The jq package that is also included is a JSON parser, which helps
with OAuth authentication when some CI systems use this image. A stable
version of OpenJDK provides a limited Java runtime environment: this isn't
built, but extracted directly from one of the official OpenJDK Docker images.

Note that the Gemfile and Gemfile.lock files determine the Jekyll build, and
are also in the final built image.

The particular combination of tools in this image is useful for Bootstrap
builds.

The .github/workflows subdirectory configures automated builds using Github
Actions, and automated publishing of the images on Docker Hub. In this case,
you must pre-define secrets on the Github repository for use with a Docker Hub
repository:
- DOCKER_ORG the Docker Hub organization to publish the image.
- DOCKER_USERNAME the Docker Hub username with access to a repository there.
- DOCKER_PASSWORD the access token to authenticate the Docker Hub user.
The Docker Hub repository name comes from the Github repository name, so the
two should use compatible conventions. Manual local builds of the image should
still work without these CI features.
