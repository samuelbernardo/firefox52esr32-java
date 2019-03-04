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

# Additional tools
RUN set -x && \
    apt-get update && \
    apt-get install -y \
        bzip2 \
        zip \
        x11vnc xvfb openbox \
        tzdata sudo bash-completion

# Install JDK 8
RUN echo "oracle-java8-installer shared/accepted-oracle-license-v1-1 select true" | debconf-set-selections
RUN echo "oracle-java8-installer shared/accepted-oracle-license-v1-1 seen true" | debconf-set-selections
RUN set -x \
    && apt-get update \
    && apt-get install -y \
        ca-certificates-java \
        default-jre \
        oracle-java8-installer \
    && wget https://github.com/samuelbernardo/firefox52esr32-java/raw/master/jre/jre-8u77-linux-i586.tar.gz \
    && mkdir /opt/jre \
    && tar -zxf jre-8u77-linux-i586.tar.gz -C /opt/jre \
    && rm jre-8u77-linux-i586.tar.gz \
    && update-alternatives --install /usr/bin/java java /opt/jre/jre1.8.0_77/bin/java 2000 \
    && echo 0 | update-alternatives --config java

# RUN echo 2 | update-alternatives --config java
# RUN java -version && update-alternatives --display java

# Install firefox
RUN set -x \
    && apt-get update \
    && apt-get install -y firefox-esr \
    && wget https://ftp.mozilla.org/pub/mozilla.org/firefox/releases/45.0.2/linux-i686/en-US/firefox-45.0.2.tar.bz2 \
    && tar -xjvf firefox*.tar.bz2 -C /opt \
    && rm firefox*.tar.bz2 \
    && ln -sf /opt/firefox/firefox /usr/bin/firefox

# RUN apt-cache policy firefox-esr | grep Installed | sed -e "s/Installed/Firefox/"

# Autostart firefox (might not be the best way to do it, but it does the trick)
RUN bash -c 'useradd -m -s /bin/bash firefox' \
    && bash -c 'usermod -aG sudo,audio,video,uucp,cdrom,plugdev firefox' \
    && bash -c 'echo "exec openbox-session &" >> ~firefox/.xinitrc' \
    && bash -c 'echo "firefox" >> ~firefox/.xinitrc' \
    && bash -c 'chown firefox:firefox ~firefox/.xinitrc' \
    && bash -c 'chmod 755 ~firefox/.xinitrc'

# Run by default firefox when container is launched
#CMD firefox-esr
CMD firefox
