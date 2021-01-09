FROM ubuntu:20.04

LABEL maintainer="Jayanga Dissanayake <jsdjayanga@gmail.com>"

ARG JAVA_HOME=/software/jdk11/jdk-11.0.9.1+1
ARG MAVEN_HOME=/software/mvn363/apache-maven-3.6.3
ARG PATH=${PATH}
ARG MOTD=" \n\
      _                    _ _   ____                 _                                  _    \n\
     | | __ ___   ____ _  / / | |  _ \  _____   _____| | ___  _ __  _ __ ___   ___ _ __ | |_  \n\
  _  | |/ _` \ \ / / _` | | | | | | | |/ _ \ \ / / _ \ |/ _ \| '_ \| '_ ` _ \ / _ \ '_ \| __| \n\
 | |_| | (_| |\ V / (_| | | | | | |_| |  __/\ V /  __/ | (_) | |_) | | | | | |  __/ | | | |_  \n\
  \___/ \__,_| \_/ \__,_| |_|_| |____/ \___| \_/ \___|_|\___/| .__/|_| |_| |_|\___|_| |_|\__| \n\
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

RUN wget https://github.com/AdoptOpenJDK/openjdk11-binaries/releases/download/jdk-11.0.9.1%2B1/OpenJDK11U-jdk_x64_linux_hotspot_11.0.9.1_1.tar.gz && \
    wget https://downloads.apache.org/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.tar.gz && \
    mkdir -p software/jdk11 && \
    mkdir -p software/mvn363 && \
    tar zxvf OpenJDK11U-jdk_x64_linux_hotspot_11.0.9.1_1.tar.gz -C software/jdk11 && \
    tar zxvf apache-maven-3.6.3-bin.tar.gz -C software/mvn363 && \
    rm -f OpenJDK11U-jdk_x64_linux_hotspot_11.0.9.1_1.tar.gz \
    rm -f apache-maven-3.6.3-bin.tar.gz

USER ubuntu
WORKDIR /home/ubuntu
ENV JAVA_HOME=${JAVA_HOME} PATH=${JAVA_HOME}/bin:${MAVEN_HOME}/bin:${PATH}
