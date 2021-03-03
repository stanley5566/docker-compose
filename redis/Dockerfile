FROM centos:7

ARG DOWNLOAD_PATH=/root/soft
RUN yum   update; \
    yum   install -y gcc automake autoconf libtool make wget; \
    mkdir $DOWNLOAD_PATH && cd $DOWNLOAD_PATH;

WORKDIR $DOWNLOAD_PATH
RUN wget -c https://download.redis.io/releases/redis-4.0.11.tar.gz; \
    tar xzvf redis-4.0.11.tar.gz; \
    cd redis-4.0.11 && make; \
    cd src && make all;

ENV REDIS_PATH=/usr/local/redis
WORKDIR redis-4.0.11/src
RUN mkdir ${REDIS_PATH} ${REDIS_PATH}/bin ${REDIS_PATH}/etc; \
    cp redis-cli redis-server redis-benchmark redis-check-aof redis-check-rdb redis-sentinel ${REDIS_PATH}/bin;

RUN mkdir /var/lib/redis;

ENV PATH=$PATH:${REDIS_PATH}/bin

WORKDIR /

ENTRYPOINT [ "/bin/sh", "-c", "redis-server ${REDIS_PATH}/etc/redis.conf --daemonize no" ]
