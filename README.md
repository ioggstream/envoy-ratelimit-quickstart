# Envoy-proxy in Docker Compose

A docker compose running envoy-proxy with the global ratelimiter enabled.

This is derived from the following 
[envoy docs](https://www.envoyproxy.io/docs/envoy/latest/start/sandboxes/front_proxy.html)

## Run

Just 

```
docker-compose up -d 
```


Test

```
curl http://localhost:8080/service/1
```

results in a response with ratelimit-headers.

```
$ curl http://localhost:8080/service/1 -i
HTTP/1.1 200 OK
content-type: text/html; charset=utf-8
content-length: 92
server: envoy
date: Fri, 07 Aug 2020 13:57:11 GMT
x-envoy-upstream-service-time: 1
x-ratelimit-limit: 50, 50;w=60
x-ratelimit-remaining: 48
x-ratelimit-reset: 0

Hello from behind Envoy (service 1)! hostname: ac2ef78fcf98 resolvedhostname: 192.168.240.5

```
