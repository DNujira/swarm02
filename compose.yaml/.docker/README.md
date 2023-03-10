# อธิบาย docker-compose.yaml

- **image: traefik:2.6**

    - เป็นการกำหนด image ของ Docker คือ traefik
    
- **ports: - "88:88"**
 
    - กำหนด port ไว้ที่ port 88
    
- **volumes: - /var/run/docker.sock:/var/run/docker.sock**

    - เป็นการให้ volume เชื่อมต่อกับ service ที่ frontend โดย path นี้

## ขั้นตอนการสร้าง backend

1.กำหนดตัว build โดยใช้ dockerfile  ที่อยู่ใน directory ชื่อ backend โดยให้เลือกไฟล์ dev.envs

2.mount volume ระหว่าง /var/run/docker.sock ใน host กับใน /var/run/docker.sock container  เพื่อให้ container สามารถเข้าถึง docker daemon ของ host ได้

- **traefik.http.routers.go.rule=Path(`/`)**

    - กำหนดให้ชี้ไปที่ไฟล์ .go จะใช้งานแล้วก็ เชื่อมต่อกับ http request ที่ path หรือว่า root path ของ domain

- **traefik.http.services.go.loadbalancer.server.port=80**

    - กำหนดให้ traefik ใช้ port 80
