# Nginx reverse proxy setup for Home Manager

## Directory structure
```
nginx
|-- docker-compose.yml
|-- certs
|   |-- domain.com.crt
|   |-- domain.com.key
|-- vhost
|   |-- domain.com_location
```

### docker-compose.yml
```yaml
version: "3"

services:
  nginx-proxy:
    image: jwilder/nginx-proxy:alpine
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - /var/run/docker.sock:/tmp/docker.sock:ro
      - ./certs:/etc/nginx/certs
      - ./vhost:/etc/nginx/vhost.d
      - vol_static:/static:ro
    networks:
      - lan

volumes:
  vol_static:
    external: true

networks:
  lan:
    external: true
```

### vhost/example.com_location
```
location /static {
  alias /static;
}
```
