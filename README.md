# Ref (traefik-golang) 
- https://github.com/docker/awesome-compose/tree/master/traefik-golang

# Wakatime swarm02
- https://wakatime.com/@spcn18/projects/jbjoorxblb

# URL (traefik-golang)
- https://github.com/docker/awesome-compose/tree/master/traefik-golang
 
## ขั้นตอนการเตรียมเครื่องมือและขั้นตอนติดตั้งอยู่ใน swarm01

https://github.com/DNujira/swarm01

# Create traefik-golang

**สร้าง image สำหรับการเตรียม push ขึ้น Docker hub**
```
sudo docker images  //เพื่อดู images ที่มีอยู่
```
**Login Docker Hub กับ work2**
```
docker login  //หลังจากใช้คำสั่งนี้ให้ใส่ username และ password ของ Docker Hub ที่ต้องการ**
```
**deploy docker**
```
sudo docker compose up -d
```
**กำหนด Tag**
```
docker tag swarm02-backend dnujira/swarm02-backend:sw02
```
**Push ไปที่ Docker Hub ที่ Login ไว้**
```
docker push swarm02-backend:sw02
```
![image](https://user-images.githubusercontent.com/117592447/224512917-d00607a3-9335-4941-aead-b1ed02f88913.png)

**Add Stack ใน Portainer**

(https://portainer.ipv9.me/)
![image](https://user-images.githubusercontent.com/117592447/224512961-8f66e9c1-aa5d-40fa-bfc9-4da55294df1b.png)

**โดยใช้โค้ด**
```
version: '3.3'
services:
  test-volume:
    image: dnujira/swarm02-backend:sw02
    networks:
     - webproxy
    logging:
      driver: json-file
    deploy:
      replicas: 1
      labels:
        - traefik.docker.network=webproxy
        - traefik.enable=true
        - traefik.http.routers.${APPNAME}-https.entrypoints=websecure
        - traefik.http.routers.${APPNAME}-https.rule=Host("${APPNAME}.xops.ipv9.me")
        - traefik.http.routers.${APPNAME}-https.tls.certresolver=default
        - traefik.http.services.${APPNAME}.loadbalancer.server.port=80
      resources:
        reservations:
          cpus: '0.1'
          memory: 6M
        limits:
          cpus: '0.4'
          memory: 40M
networks:
  webproxy:
    external: true
```
![image](https://user-images.githubusercontent.com/117592447/224513008-63044b83-e279-4379-a2e9-c3059250befa.png)

**ทดลองเข้าเพื่อดูผลลัพธ์ของ image ที่เลือกได้โดยใช้ host ที่เราตั้งไว้**

https://nujiwhale.xops.ipv9.me/
![image](https://user-images.githubusercontent.com/117592447/224513029-02cc54ce-9bdf-4a22-9149-79a87d981825.png)
