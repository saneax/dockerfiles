#
# Oracle Java 7 32 bit with icedtea-web and firefox Dockerfile
#

# Pull base image.
FROM debian

# Install Java.
RUN sed -i.bak 's/jessie main/jessie main contrib/g' /etc/apt/sources.list && \
  dpkg --add-architecture i386 && \
  apt-get update && \
  apt-get install -y libc6:i386 zlib1g:i386 && \
  apt-get install -y icedtea-7-plugin:i386 openjdk-7-jdk:i386 && \
  apt-get install -y \
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

COPY local.conf /etc/fonts/local.conf

#RUN \
#  mkdir -p /root/.mozilla/plugins && \


ENTRYPOINT [ "/usr/bin/iceweasel" ]
