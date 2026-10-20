# MeshCentral за nginx proxy manager 

## Команды  
docker compose  down  
docker compose up --build -d --remove-orphans --force-recreate && docker-compose logs -f

## Nginx proxy manager
Custom Nginx Configuration  
``` 
location / {
    proxy_ssl_verify off;
    proxy_pass $forward_scheme://$server:$port;
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto $scheme;
    
    # Для поддержки WebSocket (MeshCentral требует)
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection $http_connection;
}
```
