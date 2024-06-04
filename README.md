# openSUSE Build Environment Maven Images

This project builds a number of openSUSE-based images that include various versions of JDK, Dotnet and Mono commands along with Maven. They are intended to be used to build other images.

The images which are built in this project are:
- buildenv-jdk8
- buildenv-jdk11
- buildenv-jdk17
  - buildenv-dotnet
    - buildenv-dotnet-mono

### Usage

#### As an SEPG Build Environment Image
The Docker image should be specified in the `official-build.props` file:
```
SEPG_BUILD_ENV_IMAGE=cafapi/buildenv-jdk17:4.0.0
```

### Local Use
The image can also be used locally, for example in a WSL environment.

Create a convenience function along the following lines - you may wish to vary some details to suit your environment:
```
function buildenv-jdk17 {
  local cDrive;
  local userProfile;
  local wslUserProfile="$(wslpath "$(cmd.exe /C "echo | set /p=%USERPROFILE%" 2>/dev/null)")";

  # Set variables for WSL 1 or for WSL 2
  if [[ -n "${WSL_INTEROP}" ]]; then
    cDrive='/mnt/c';
    userProfile="${wslUserProfile}";
  else
    cDrive='/run/desktop/mnt/host/c';
    userProfile=$(echo ${wslUserProfile} | sed -E 's#^/mnt/#/run/desktop/mnt/host/#');
  fi

  docker container run -it --rm \
    --network=host \
    -h buildenv-jdk17 \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v "${cDrive}":/mnt/c \
    -v buildenv-dotnet-mono_home:/root \
    -v "${userProfile}"/.gnupg:/root/.gnupg \
    -v "${userProfile}"/.m2:/root/.m2 \
    -e HTTP_PROXY -e HTTPS_PROXY -e NO_PROXY \
    -e http_proxy -e https_proxy -e no_proxy \
    -w "$(pwd)" \
    cafapi/buildenv-jdk17:4.0.0 "$@";
}
```

You can use the function to run tools that are in the build environment image:
```
