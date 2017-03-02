FROM 10.64.88.16/erlang:v1

MAINTAINER Cuenca Inteligente 

ADD ./start.sh /start.sh

ENV EMQ_VERSION=v2.1 
ENV ADMIN_DASH_USER=oiot
ENV ADMIN_DASH_PASS=oiot

ENV EMQ_NODE_COOKIE=emq_dist_cookie
ENV EMQ_PROCESS_LIMIT=2097152
ENV EMQ_MAX_PORTS=1048576
ENV EMQ_LOG_CONSOLE=file
ENV EMQ_LOG_LEVEL=error
ENV EMQ_ALLOW_ANONYMOUS=true
ENV EMQ_TCP_PORT=1883
ENV EMQ_TCP_ACCEPTORS=64
ENV EMQ_TCP_MAX_CLIENTS=1000000
ENV EMQ_SSL_PORT=8883
ENV EMQ_SSL_ACCEPTORS=32
ENV EMQ_SSL_MAX_CLIENTS=500000
ENV EMQ_HTTP_PORT=8083
ENV EMQ_HTTP_ACCEPTORS=64
ENV EMQ_HTTP_MAX_CLIENTS=1000000
ENV EMQ_HTTPS_PORT=8084
ENV EMQ_HTTPS_ACCEPTORS=32
ENV EMQ_HTTPS_MAX_CLIENTS=500000
ENV EMQ_MAX_PACKET_SIZE=64KB


RUN apk update

RUN apk --no-cache add \ 
	git \
	make \
	musl \
	gcc \
    build-base \
    ncurses-terminfo-base \
    ncurses-terminfo \
    ncurses-libs \
    readline \	
	perl \
	wget \
	&& wget https://github.com/rebar/rebar/wiki/rebar -O /rebar \
    && chmod +x rebar \
    && cp /rebar /bin/ \
	&& git clone -b ${EMQ_VERSION} https://github.com/emqtt/emq-relx.git /emqttd \
	&& cd /emqttd \
	&& make \
	&& mkdir /opt && mv /emqttd/_rel/emqttd /opt/emqttd \
	&& cd / && rm -rf /emqttd \
	&& mv /start.sh /opt/emqttd/start.sh \
	&& chmod +x /opt/emqttd/start.sh

RUN apk --purge del \
	git \
    make \
    musl \
    gcc \
    build-base \
    ncurses-terminfo-base \
    ncurses-terminfo \
    ncurses-libs \
    readline \	
	wget \
	perl	

RUN rm -rf /var/cache/apk/*	

WORKDIR /opt/emqttd 

# start emqttd and initial environments
CMD ["/opt/emqttd/start.sh"]

VOLUME ["/opt/emqttd/log", "/opt/emqttd/data", "/opt/emqttd/plugins", "/opt/emqttd/etc"]

# emqttd will occupy these port:
# - 1883 port for MQTT
# - 8883 port for MQTT(SSL)
# - 8083 for WebSocket/HTTP
# - 8084 for WSS/HTTPS
# - 18083 for dashboard
# - 4369 for port mapping
# - 6000-6999 for distributed node

#DESARROLLO
#EXPOSE 1883 8883 8083 8084 18083 4369 6000-6999

#PRODUCCION
EXPOSE 1883 8883 18083 
