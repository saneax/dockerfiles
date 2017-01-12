#
# Oracle Java 7 32 bit with icedtea-web and firefox Dockerfile
#

# Pull base image.
FROM 32bit/ubuntu:14.04
MAINTAINER Sanjay Upadhyay "saneax@gmail.com"

RUN  apt-get update && apt-get install -y \
	bzip2 \
	ca-certificates \
	curl \
	flashplugin-nonfree \
	hicolor-icon-theme \
	libasound2 \
	libdbus-glib-1-2 \
	libgl1-mesa-dri \
	libgl1-mesa-glx \
  software-properties-common \
  sudo \
  vim \
  screen \
  libgtk2-perl \
  libwww-perl && \
  rm -rf /var/lib/apt/lists/*

COPY local.conf /etc/fonts/local.conf

RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 16126D3A3E5C1192  && \
   apt-key adv --keyserver keyserver.ubuntu.com --recv-keys C2518248EEA14886 && \
  apt-get update && \
  apt-get install libxtst6 rsync -y


# Install Java.
RUN \
  echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
  add-apt-repository -y ppa:webupd8team/java && \
  apt-get update && \
  apt-get install -y oracle-java8-installer && \
  rm -rf /var/lib/apt/lists/* && \
  rm -rf /var/cache/oracle-jdk8-installer


ENV FIREFOX_VERSION 39.0
ENV LANG en-US
ENV ARCH i686

RUN curl -sSL "https://ftp.mozilla.org/pub/mozilla.org/firefox/releases/${FIREFOX_VERSION}/linux-${ARCH}/${LANG}/firefox-${FIREFOX_VERSION}.tar.bz2" -o /tmp/firefox.tar.bz2 \
	&& mkdir -p /opt/firefox \
	&& tar -xjf /tmp/firefox.tar.bz2 -C /opt/firefox --strip-components 1 \
	&& rm /tmp/firefox.tar.bz2* \
	&& ln -s /opt/firefox/firefox /usr/bin/firefox


RUN useradd -ms /bin/bash -G sudo -p onevision sanjayu
RUN chown -R sanjayu:sanjayu /home/sanjayu
ENV HOME /home/sanjayu

RUN cd /home/sanjayu && \
  wget -q -O /tmp/msjnc https://raw.github.com/madscientist/msjnc/master/msjnc && \
  chmod 755 /tmp/msjnc && \
  cp /tmp/msjnc /usr/bin

RUN usermod --password onevision sanjayu && \
  sudo rm -rf /var/lib/apt/lists/* && \
  apt-get update && \
  apt-get install unzip -y

USER sanjayu

RUN \
  mkdir -p /home/sanjayu/.mozilla/plugins && \
  ln -s /usr/lib/jvm/java-8-oracle/jre/lib/i386/libnpjp2.so /home/sanjayu/.mozilla/plugins/


WORKDIR /home/sanjayu

# Define commonly used JAVA_HOME variable
ENV JAVA_HOME /usr/lib/jvm/java-8-oracle


ENTRYPOINT [ "/usr/bin/firefox" ]
