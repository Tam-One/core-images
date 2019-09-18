FROM node:8.16-alpine

# Set timezone
ENV TZ=Europe/Amsterdam

RUN apk --update add \
		  tzdata && \
	cp /usr/share/zoneinfo/$TZ /etc/localtime && \
    echo $TZ > /etc/timezone

# Add build dependencies to virtual group
RUN apk --no-cache --virtual temp add build-base \
                       autoconf \
                       curl

# Required dependencies
RUN apk --no-cache add zeromq-dev \
                       python2 && \
                       build-base && \
    curl -Ls "https://github.com/dustinblackman/phantomized/releases/download/2.1.1/dockerized-phantomjs.tar.gz" | tar xz -C

# Set python env variable
ENV PYTHON /usr/bin/python2

WORKDIR /home/node/app

# Delete build dependencies
RUN apk del temp

# Create directories
RUN mkdir /home/node/dists && \
    mkdir /home/node/dists/recordings && \
    mkdir /home/node/dists/qooqie && \
    mkdir /home/node/certs

ENTRYPOINT ["node", "app.js"]
