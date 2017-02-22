FROM 10.64.88.16/erlang:v1

MAINTAINER Cuenca Inteligente 

ADD ./start.sh /start.sh

ENV EMQ_VERSION=v2.0.3 

RUN apk update

RUN apk --no-cache add \ 
	git \
	make \
	perl \
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

EXPOSE 1883 8883 8083 8084 18083 4369 6000-6999
