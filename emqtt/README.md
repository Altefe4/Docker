
Docker de EMQTT

===

Docker para ejecutar el broker EMQTT. El contenedor utiliza como base al de Erlang

===

```bash

docker build --build-arg http_proxy=http://<IP_PROXY>:3128 --build-arg https_proxy=http://<IP_PROXY>:3128 -t <IP_REGISTRY>/emqtt:v1 .

Puertos que utiliza

# - 1883 port for MQTT
# - 8883 port for MQTT(SSL)
# - 8083 for WebSocket/HTTP
# - 8084 for WSS/HTTPS
# - 18083 for dashboard

```bash
docker run -d --name=emqtt -p 1883:1883 -p 8883:8883 -p 8083:8083 -p 18083:18083 -p 8084:8084 -v /opt/emqttd/log:/opt/emqttd/log -v /opt/emqttd/data:/opt/emqttd/data -v /opt/emqttd/plugins:/opt/emqttd/plugins -v /opt/emqttd/etc:/opt/emqttd/etc 10.64.88.16/emqtt:v1

