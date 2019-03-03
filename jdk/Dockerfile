FROM i386/ubuntu:xenial

RUN add-apt-repository ppa:webupd8team/java
RUN add-apt-repository ppa:jonathonf/firefox-esr-52

RUN set -x \
    && apt-get update \
    && apt-get install -y \
        locales

ENV LANG en_US.utf8
RUN locale-gen $LANG

# Install JDK 8
RUN set -x \
    && apt-get update \
    && apt-get install -y \
        ca-certificates-java \
        default-jdk \
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
        zip

# RUN java -version
# RUN apt-cache policy firefox-esr | grep Installed | sed -e "s/Installed/Firefox/"