#
# Oracle Java 7 32 bit with icedtea-web and firefox Dockerfile
#

# Pull base image.
FROM 32bit/debian:jessie

# Install Java.
RUN sed -i.bak 's/jessie main contrib/jessie main/g' /etc/apt/sources.list && \
  apt-get update && \
  apt-get install -y debian-archive-keyring && \
  apt-key update && \
  apt-get update


RUN  apt-get install -y \
	bzip2 \
	ca-certificates \
	curl \
	flashplugin-nonfree \
	hicolor-icon-theme \
	libasound2 \
	libdbus-glib-1-2 \
	libgl1-mesa-dri \
	libgl1-mesa-glx \
  iceweasel --no-install-recommends && \
  rm -rf /var/lib/apt/lists/*

RUN apt-get install -y libc6 zlib1g

RUN apt-get install -y icedtea-7-plugin openjdk-7-jdk

COPY local.conf /etc/fonts/local.conf

#RUN \
#  mkdir -p /root/.mozilla/plugins && \


ENTRYPOINT [ "/usr/bin/iceweasel" ]
