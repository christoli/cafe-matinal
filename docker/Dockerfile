FROM ubuntu:16.04

MAINTAINER Paapa Abdullah Morgan <paapaabdullahm@gmail.com>

ENV DEBIAN_FRONTEND=noninteractive \
    ANDROID_HOME=/opt/android-sdk-linux \
    NODE_VERSION=9.11.1 \
    NPM_VERSION=5.8.0 \
    IONIC_VERSION=3.20.0 \
    CORDOVA_VERSION=7.1.0

#BASIC STUFF && ENVIRONMENT PREPARATION
RUN echo ANDROID_HOME="${ANDROID_HOME}" >> /etc/environment \
    && dpkg --add-architecture i386 \
    && apt-get update \
    && apt-get install -y python-software-properties software-properties-common build-essential git wget curl unzip ruby \
    && git config --global user.email "full3right@gmail.com" \
    && git config --global user.name "Full Bright" \
    && add-apt-repository -y ppa:webupd8team/java \
    && curl -sL https://deb.nodesource.com/setup_9.x -o nodesource_setup.sh \
    && bash nodesource_setup.sh \
    && apt-get install -y nodejs \
    && npm install -g npm@"$NPM_VERSION" \
    && npm install -g cordova@"$CORDOVA_VERSION" ionic@"$IONIC_VERSION" \
    && npm install -g sass    

# START THE APPLICATION
RUN ionic start myApp sidemenu --no-link --cordova


#JAVA STUFF
#RUN add-apt-repository -y ppa:webupd8team/java \
RUN echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections \
    && apt-get install -y oracle-java8-installer

#ANDROID STUFF
#RUN echo ANDROID_HOME="${ANDROID_HOME}" >> /etc/environment \
RUN apt-get install -y --force-yes expect ant wget libc6-i386 lib32stdc++6 lib32gcc1 lib32ncurses5 lib32z1 qemu-kvm kmod \
    && apt-get clean \
    && apt-get autoclean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && rm -rf /var/cache/oracle-jdk8-installer \
    && cd /opt \
    && wget --output-document=android-sdk.tgz --quiet http://dl.google.com/android/android-sdk_r24.4.1-linux.tgz \
    && tar xzf android-sdk.tgz \
    && rm -f android-sdk.tgz \
    && chown -R root. /opt

# GRADLE INSTALLATION
RUN cd /opt \
    && wget --output-document=gradle-4.7-bin.zip --quiet https://services.gradle.org/distributions/gradle-4.7-bin.zip \
    && unzip -d /opt/gradle gradle-4.7-bin.zip \
    && chown -R root. /opt

ENV PATH ${PATH}:${ANDROID_HOME}/tools:${ANDROID_HOME}/platform-tools:/opt/tools:/opt/gradle/gradle-4.7/bin

#UPDATE SDK
COPY docker/tools /opt/tools

RUN chmod -R +x /opt/tools/android-accept-licenses.sh

RUN ["/opt/tools/android-accept-licenses.sh", "android update sdk --all --no-ui --filter platform-tools,tools,build-tools-23.0.2,android-23,extra-android-support,extra-android-m2repository,extra-google-m2repository"]
RUN unzip ${ANDROID_HOME}/temp/*.zip -d ${ANDROID_HOME}

WORKDIR myApp
EXPOSE 8100 35729
CMD ["ionic", "lab"]
