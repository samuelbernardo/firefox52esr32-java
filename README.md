# References

The dockerfiles in this project were built reviewing the code of [docker-node-jdk-chrome-firefox](https://bitbucket.org/atlassian/docker-node-jdk-chrome-firefox/) and of [docker-firefox-java](https://github.com/ktelep/docker-firefox-java).

# Dockerfile purpose

This dockerfile allows to run a container with Firefox 52 ESR 32bit and JRE 8.

Firefox 52 ESR 32bit is the latest version to support Java and is useful for web applets that still needs to run from web server.

# Contents

This docker file contains:
- Ubuntu 16.04
- Firefox 52 ESR 32bit (insecure since it's not supported anymore)
- JRE 8 (with tag JRE)
- JDK 8 (with tag JDK)

# How to build the image

## Docker image with JRE

Docker file is in directory jre inside git repository.

`docker build -t firefox52esr32-java-jre <PROJECT_DIR>/jre`

then use `docker images` to find image ID.

With the following command

`docker run -it --rm --net=host --env="DISPLAY=unix$DISPLAY" --privileged --env="QT_X11_NO_MITSHM=1" --volume="$HOME/.Xauthority:/home/firefox/.Xauthority:rw" --volume "/tmp/.X11-unix:/tmp/.X11-unix" <IMAGE_ID>`

you can test if your changes are the desired ones.

Then tag it: `docker tag <IMAGE_ID> <YOUR-USER>/firefox52esr32-java:jre` and finally publish it: `docker push <YOUR-USER>/firefox52esr32-java:jre`.


## Docker image with JDK

Docker file is in directory jdk inside git repository.

`docker build -t firefox52esr32-java-jdk <PROJECT_DIR>/jdk`

then use `docker images` to find image ID.

With the following command

`docker run -it --rm --net=host --env="DISPLAY=unix$DISPLAY" --privileged --env="QT_X11_NO_MITSHM=1" --volume="$HOME/.Xauthority:/home/firefox/.Xauthority:rw" --volume "/tmp/.X11-unix:/tmp/.X11-unix" <IMAGE_ID>`

you can test if your changes are the desired ones.

Then tag it: `docker tag <IMAGE_ID> <YOUR-USER>/firefox52esr32-java:jdk` and finally publish it: `docker push <YOUR-USER>/firefox52esr32-java:jdk`.
