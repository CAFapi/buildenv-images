# openSUSE JDK11 Maven Build Image

This project creates an openSUSE-based image that includes the JDK 11 and Maven.  It is intended to be used to build other images.

This command can be used to create an convenience alias for using this image:

    alias mvn='docker container run -it --rm --network=host -e HTTP_PROXY -e HTTPS_PROXY -e NO_PROXY -v ~/.m2:/root/.m2 -v /var/run/docker.sock:/var/run/docker.sock -v $(pwd):/wd -w /wd cafapi/buildenv-jdk11 mvn'

### Usage

#### As an SEPG Build Environment Image
The Docker image should be specified in the `official-build.props` file:
```
SEPG_BUILD_ENV_IMAGE=cafapi/buildenv-jdk11:4.0.0
```
