### Ref 
https://github.com/docker/awesome-compose/tree/master/plex

### wakatime swarm02
https://wakatime.com/@spcn12/projects/offfhsprcp


### Create VM template 3 node (manager, work1,work2)
  * Os Ubuntu 22.04
  * Cpu 2 core
  * Memory 2024 MB
  * Storege 32 GB

### requrement
  * Docker
  * Wakatime
  * Github
  * Folder swarm01, swarm02 (managernode) choose app frome Reference to swarm01 floder
  
### BUILD-IMAGE --> TAG ---> LOGIN DOCGER IN VM --> PUSH TO DOCKER
  * Build images
  * cd to path folder swarm01 and run this command
```
sudo docker compose "django/compose.yaml" up -d --build
```
  * Tag images 
```
  sudo docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]
```
  * Login to docker
```
  docker login
```
  * Push to docker
```
  docker push TARGET_IMAGE[:TAG]
```

### Create stack deploy
  * Create file docker=coompose.yml in swarm path
```
version: '3.3' 
services:
  web: 
    image: kantapongkk/plex:v1
    networks: 
    - webproxy 
    logging:
      driver: json-file
    container_name: spcn12plex
    deploy: 
      replicas: 1
      labels: 
        - traefik.docker.network=webproxy
        - traefik.enable=true
        - traefik.http.routers.spcn12plex-https.entrypoints=websecure 
        - traefik.http.routers.spcn12plex-https.rule=Host("spcn12plex.xops.ipv9.xyz")
        - traefik.http.routers.spcn12plex-https.tls.certresolver=default
        - traefik.http.services.spcn12plex.loadbalancer.server.port=32400 
      resources: 
        reservations: 
          cpus: '0.1'
          memory: 10M
        limits: 
          cpus: '0.4'
          memory: 170M
networks: 
  webproxy: 
    external: true
```
  * stack de ploy on portainer
  * go to view result
```
spcn12plex.xops.ipv9.xyz
```

![image](https://github.com/Kantapong11755/swarm02/blob/master/plex.png)
  
  
  
  
  
  
  

