FROM armv7/armhf-ubuntu:16.04

ARG HOSTNAME
ARG DOCKER_GROUP_GID
ARG RUNDECK_USER_GID
ARG RUNDECK_GROUP_GID
ARG RUNDECK_VERSION

RUN groupadd --gid $DOCKER_GROUP_GID docker
RUN groupadd --gid $RUNDECK_GROUP_GID rundeck
RUN useradd --uid $RUNDECK_USER_GID --gid $RUNDECK_GROUP_GID rundeck
RUN usermod -a -G docker rundeck

RUN apt-get update -y -q                                                                                        \
    && apt-get install -y -q sudo curl expect git-core net-tools socat dosfstools iputils-ping netcat docker.io \
    && apt-get clean                                                                                            \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /opt
RUN curl -fsSL http://www.java.net/download/java/jdk8u112/archive/b04/binaries/jdk-8u112-ea-bin-b04-linux-arm-vfp-hflt-25_jul_2016.tar.gz | tar -xzv

RUN mkdir /opt/rundeck
WORKDIR /opt/rundeck
RUN curl -fsSL http://dl.bintray.com/rundeck/rundeck-maven/rundeck-launcher-$RUNDECK_VERSION.jar > rundeck-launcher.jar

ENV JAVA_HOME /opt/jdk1.8.0_112
ENV PATH ${JAVA_HOME}/bin:${PATH}

RUN chown rundeck:rundeck -R /opt/rundeck
USER rundeck
WORKDIR /opt/rundeck

RUN java -jar rundeck-launcher.jar --installonly
RUN echo "grails.serverURL=http://$HOSTNAME:4440" >> server/config/rundeck-config.properties

EXPOSE 4440
CMD java -Xmx512m -Xms128m -server -jar rundeck-launcher.jar
