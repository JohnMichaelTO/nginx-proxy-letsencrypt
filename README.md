# Nginx reverse proxy with Let's encrypt SSL certificate

This is a simple repo containing a docker compose file to run an nginx reverse proxy with a let's encrypt SSL certificate.

More details can be found [here](https://github.com/nginx-proxy/acme-companion).

To attach another docker container, you simply need to run another docker compose with a file containing this:
```yml
version: "3.5"

services:
  my-service:
    image: nginx:1.19-alpine
    ports:
      - "80:80"
    networks:
      - other_network
      - backend
    environment:
      VIRTUAL_HOST: "subdomain.domain.com"
      LETSENCRYPT_HOST: "subdomain.domain.com"
      LETSENCRYPT_EMAIL: "my@email.com"

networks:
  other_network:
  backend:
    external: true
    name: nginxproxy-letsencrypt_backend
```
