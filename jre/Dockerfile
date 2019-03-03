FROM f69m/ubuntu32:xenial

# Install required tools and repositories
ENV DEBIAN_FRONTEND noninteractive
RUN set -x \
    && apt-get update \
    && apt-get install -y \
        apt-utils \
        debconf-utils \
        software-properties-common

RUN add-apt-repository ppa:webupd8team/java
RUN add-apt-repository ppa:jonathonf/firefox-esr-52

RUN set -x \
    && apt-get update \
    && apt-get install -y \
        locales

ENV LANG en_US.utf8
RUN locale-gen $LANG

# Install JDK 8
RUN echo "oracle-java8-installer shared/accepted-oracle-license-v1-1 select true" | debconf-set-selections
RUN echo "oracle-java8-installer shared/accepted-oracle-license-v1-1 seen true" | debconf-set-selections
RUN set -x \
    && apt-get update \
    && apt-get install -y \
        ca-certificates-java \
        default-jre \
        oracle-java8-installer

#RUN echo 2 | update-alternatives --config java

# Install firefox
RUN set -x \
    && apt-get update \
    && apt-get install -y \
        firefox-esr

# Additional tools
RUN set -x && \
    apt-get update && \
    apt-get install -y \
        bzip2 \
        zip \
        x11vnc xvfb openbox \
        tzdata

# RUN java -version
# RUN apt-cache policy firefox-esr | grep Installed | sed -e "s/Installed/Firefox/"

# Autostart firefox (might not be the best way to do it, but it does the trick)
RUN bash -c 'echo "exec openbox-session &" >> ~/.xinitrc' \
    && bash -c 'echo "firefox" >> ~/.xinitrc' \
    && bash -c 'chmod 755 ~/.xinitrc'
