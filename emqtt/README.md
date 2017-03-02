
Docker de EMQTT

===

Docker para ejecutar el broker EMQTT. El contenedor utiliza como base al de Erlang

===

```bash

docker build --build-arg http_proxy=http://<IP_PROXY>:3128 --build-arg https_proxy=http://<IP_PROXY>:3128 -t 10.64.88.16/emqtt:v1 .

Puertos que utiliza

# - 1883 port for MQTT
# - 8883 port for MQTT(SSL)
# - 8083 for WebSocket/HTTP
# - 8084 for WSS/HTTPS
# - 18083 for dashboard

#Desarrollo
```bash
docker run -d --name=emqtt -p 1883:1883 -p 8883:8883 -p 8083:8083 -p 18083:18083 -p 8084:8084 -v /opt/emqttd/log:/opt/emqttd/log -v /opt/emqttd/data:/opt/emqttd/data -v /opt/emqttd/plugins:/opt/emqttd/plugins -v /opt/emqttd/etc:/opt/emqttd/etc 10.64.88.16/emqtt:v1

#Producción
#Agrega el usuario del dashboard y no permite peticiones anonimas.
```bash
sudo docker run -d --name=emqtt -p 1883:1883 -p 8883:8883 -p 18083:18083 --env ADMIN_DASH_USER=ute --env ADMIN_DASH_PASS=ute --env EMQ_ALLOW_ANONYMOUS=false 10.64.88.16/emqtt:v1

