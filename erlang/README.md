
Docker de Erlang

===

Este contenedor tiene todo lo necesario para ejecutar aplicaciones hechas con Erlang. Esta básado en la versión 3.4 de ALPINE.

Este docker es utilizado por:

	- EMQTT

====

docker build --build-arg http_proxy=http://<ip_proxy>:3128 -t <DOCKER_REGISTRY>>erlang:v0 .
