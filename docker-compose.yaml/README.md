# อธิบาย docker-compose.yml
- **version: '3.3'**

  - กำหนด version ของ compose ให้เป็น version 3.3
  
- **image: dnujira/swarm02-backend:sw02**

  - กำหนด image ให้ชื่อว่า swarm02-backend:sw02 โดยเป็น image ที่เรามีอยู่ใน docker hub
  
- **networks: - webproxy**

  - กำหนด network ให้ container ชื่อ webproxy
  
 - **logging: driver: json-file**
 
    - กำหนดว่าเราจะใช้ json-file ในการเก็บ log
 
 - **deploy: replicas: 1**
 
   - กำหนดให้ deploy แค่ 1 replicas
  
  - **traefik.docker.network=webproxy**
  
    - กำหนดให้ traefik ใช้ network ที่ชื่อว่า webproxy
 
 - **traefik.http.routers.${APPNAME}-https.entrypoints=websecure**
 
    - กำหนดให้ traefik ใช้ entrypoints เป็น websecure โดยใน ${APPNAME} ตั้งชื่อเป็น nujiwhale
 
 - **traefik.http.routers.${APPNAME}-https.rule=Host("${APPNAME}.xops.ipv9.me")**
 
    - กำหนดให้ traefik ใช้ routers "nujiwhale.xops.ipv9.me" ในการ handle request
    
 - **traefik.http.routers.${APPNAME}-https.tls.certresolver=default**
 
    - กำหนดให้ traefik ใช้ certresolver ชื่อ default ในการดึง TLS โดยใน ${APPNAME} ตั้งชื่อเป็น nujiwhale
 
 - **traefik.http.services.${APPNAME}.loadbalancer.server.port=80**
 
    - กำหนดให้ traefik ใช้ port 80 โดยใน ${APPNAME} ตั้งชื่อเป็น nujiwhale
