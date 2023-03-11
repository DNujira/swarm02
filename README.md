## Ref (traefik-golang) 
- https://github.com/docker/awesome-compose/tree/master/traefik-golang

## Wakatime swarm02
- https://wakatime.com/@spcn18/projects/jbjoorxblb

## URL (traefik-golang)
- https://github.com/docker/awesome-compose/tree/master/traefik-golang
 
 **ขั้นตอนการเตรียมเครื่องมือและขั้นตอนติดตั้งอยู่ใน swarm01**

https://github.com/DNujira/swarm01

 **Compose image โดย image ที่เลือก คือ traefik-golang**
 ```
 version: '3.7'

services:
  web:
    image: dnujira/swarm02-backend:sw02
    command: --providers.docker --entrypoints.web.address=:90 --providers.docker.exposedbydefault=false
    networks:
      - traefik-public
    environment:
      - PORT=80
    volumes:
      - whale:/usr/src/app/whale
    ports:
      - "88:88"
    depends_on:
      - deploy
    deploy:
      replicas: 1
      labels:
        - traefik.docker.network=traefik-public
        - traefik.enable=true
        - traefik.http.routers.${appname}-https.entrypoints=websecure
        - traefik.http.routers.${appname}-https.rule=Host("{appname}.xops.ipv9.me")
        - traefik.http.routers.${appname}-https.tls.certresolver=default
        - traefik.http.services.${appname}.loadbalancer.server.port=80
        - "traefik.http.routers.go.rule=Path(/)"
        - "traefik.http.services.go.loadbalancer.server.port=80"
      restart_policy:
        condition: any
      update_config:
        delay: 5s
        parallelism: 1
        order: start-first
volumes:
  whale:

networks:
  default:
    driver: overlay
    attachable: true   
  traefik-public:
    external: true
```
## ยังไม่สมบูรณ์ค่ะ
