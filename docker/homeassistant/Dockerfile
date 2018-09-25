FROM debian:latest
LABEL Homeassistant with dependent python libs

MAINTAINER Oyvind Bergerud <oyvind.bergerud@gmail.com>

VOLUME /config

FROM debian:latest

# https://community.home-assistant.io/t/ikea-tradfri-gateway-zigbee-very-basic-working-implementation/14788/19?u=balloob
RUN apt-get update -y && \
  apt-get install -y python3 python3-pip git autoconf automake libtool wget && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* build/

RUN mkdir -p /usr/src/app /usr/src/build
WORKDIR /usr/src/build

RUN python3 -m pip install --upgrade pip setuptools wheel cython

RUN wget https://raw.githubusercontent.com/ggravlingen/pytradfri/master/script/install-coap-client.sh
RUN sh install-coap-client.sh

RUN wget https://raw.githubusercontent.com/ggravlingen/pytradfri/master/requirements.txt
RUN python3 -m pip install -r requirements.txt


WORKDIR /usr/src/app
RUN wget -O requirements_all.txt  https://raw.githubusercontent.com/home-assistant/home-assistant/dev/requirements_all.txt
RUN pip install -r requirements_all.txt
RUN pip install homeassistant
RUN mkdir -p /usr/src/app
EXPOSE 8123
WORKDIR /config
CMD [ "python3", "-m", "homeassistant", "--config", "/config" ]
