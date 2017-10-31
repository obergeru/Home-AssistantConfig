FROM python
LABEL Homeassistant with dependent python libs

MAINTAINER Oyvind Bergerud <oyvind.bergerud@gmail.com>

VOLUME /config

RUN apt-get update
RUN apt-get install --force-yes -y make libudev-dev g++ libyaml-dev

WORKDIR /usr/src/app
RUN pip install cython wheel six
RUN pip install 'PyDispatcher>=2.0.5'
RUN pip install python_openzwave
#ADD ./requirements.txt ./requirements.txt
RUN wget -O requirements.txt  https://raw.githubusercontent.com/home-assistant/home-assistant/dev/requirements_all.txt
RUN pip install -r requirements.txt
RUN pip install homeassistant
RUN mkdir -p /usr/src/app
EXPOSE 8123
WORKDIR /config
CMD [ "python3", "-m", "homeassistant", "--config", "/config" ]
