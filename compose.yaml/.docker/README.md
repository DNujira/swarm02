# อธิบาย docker-compose.yaml

- **image: traefik:2.6**

    - เป็นการกำหนด image ของ Docker คือ traefik
    
- **ports: - "88:88"**
 
    - กำหนด port ไว้ที่ port 88
    
- **volumes: - /var/run/docker.sock:/var/run/docker.sock**

    - เป็นการให้ volume เชื่อมต่อกับ service ที่ frontend โดย path นี้

- **traefik.http.routers.go.rule=Path(`/`)**

    - กำหนดให้ชี้ไปที่ไฟล์ .go จะใช้งานแล้วก็ เชื่อมต่อกับ http request ที่ path หรือว่า root path ของ domain

- **traefik.http.services.go.loadbalancer.server.port=80**

    - กำหนดให้ traefik ใช้ port 80
