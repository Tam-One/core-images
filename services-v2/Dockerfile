FROM node:10-alpine

# Add build dependencies to virtual group
RUN apk --no-cache --virtual temp add build-base \
                       autoconf \
                       curl

ENV TZ=Europe/Amsterdam

RUN apk --update add \
		tzdata \
	&& cp /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone \
	&& apk del tzdata \
	&& ntpd -d -q -n -p uk.pool.ntp.org

# Required dependencies
RUN apk --no-cache add zeromq-dev \
                       python2 && \
    curl -Ls "https://github.com/dustinblackman/phantomized/releases/download/2.1.1/dockerized-phantomjs.tar.gz" | tar xz -C /

# Set python env variable
ENV PYTHON /usr/bin/python2