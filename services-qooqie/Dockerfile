FROM node:8.16-alpine

# Set timezone
ENV TZ=Europe/Amsterdam

RUN apk --update add \
		  tzdata && \
	cp /usr/share/zoneinfo/$TZ /etc/localtime && \
    echo $TZ > /etc/timezone

WORKDIR /home/node/app

RUN mkdir /home/node/dists && \
    mkdir /home/node/dists/recordings && \
    mkdir /home/node/dists/qooqie && \
    mkdir /home/node/certs

ENTRYPOINT ["node", "app.js"]
