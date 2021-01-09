FROM ubuntu:20.04

LABEL maintainer="Jayanga Dissanayake <jsdjayanga@gmail.com>"

ARG JAVA_HOME=/software/jdk8/jdk8u275-b01
ARG MAVEN_HOME=/software/mvn363/apache-maven-3.6.3
ARG PATH=${PATH}
ARG MOTD=" \n\
      _                     ___    ____                 _                                  _    \n\
     | | __ ___   ____ _   ( _ )  |  _ \  _____   _____| | ___  _ __  _ __ ___   ___ _ __ | |_  \n\
  _  | |/ _` \ \ / / _` |  / _ \  | | | |/ _ \ \ / / _ \ |/ _ \| '_ \| '_ ` _ \ / _ \ '_ \| __| \n\
 | |_| | (_| |\ V / (_| | | (_) | | |_| |  __/\ V /  __/ | (_) | |_) | | | | | |  __/ | | | |_  \n\
  \___/ \__,_| \_/ \__,_|  \___/  |____/ \___| \_/ \___|_|\___/| .__/|_| |_| |_|\___|_| |_|\__| \n\
                                                               |_|                              \n\
"

RUN apt-get update && \
    apt-get install -y \
        sudo \
        netcat \
        unzip \
        wget \
        git \
        vim && \
    rm -rf /var/lib/apt/lists/*

RUN useradd -rm -d /home/ubuntu -s /bin/bash -g root -G sudo -u 1001 ubuntu -p "$(openssl passwd -1 ubuntu)" && \
    echo '[ ! -z "${TERM}" -a -r /etc/motd ] && cat /etc/motd' >> /etc/bash.bashrc; echo "${MOTD}" > /etc/motd

RUN wget https://github.com/AdoptOpenJDK/openjdk8-binaries/releases/download/jdk8u275-b01/OpenJDK8U-jdk_x64_linux_hotspot_8u275b01.tar.gz && \
    wget https://downloads.apache.org/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.tar.gz && \
    mkdir -p software/jdk8 && \
    mkdir -p software/mvn363 && \
    tar zxvf OpenJDK8U-jdk_x64_linux_hotspot_8u275b01.tar.gz -C software/jdk8 && \
    tar zxvf apache-maven-3.6.3-bin.tar.gz -C software/mvn363 && \
    rm -f OpenJDK8U-jdk_x64_linux_hotspot_8u275b01.tar.gz \
    rm -f apache-maven-3.6.3-bin.tar.gz

USER ubuntu
WORKDIR /home/ubuntu
ENV JAVA_HOME=${JAVA_HOME} PATH=${JAVA_HOME}/bin:${MAVEN_HOME}/bin:${PATH}
