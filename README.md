# Docker Nginx

Dockerized Nginx based on Alpine Linux with TLS 1.3 and Brotli support.

Inspired by:
 - [nginxinc/docker-nginx](https://github.com/nginxinc/docker-nginx)
 - [google/ngx_brotli](https://github.com/google/ngx_brotli)
 - [eustas/ngx_brotli](https://github.com/eustas/ngx_brotli)
 - [fholzer/docker-nginx-brotli](https://github.com/fholzer/docker-nginx-brotli)

## How to use this image

```shell
docker pull hackinit/nginx-brotli
docker run --name some-nginx -v /some/content:/usr/share/nginx/html:ro -d hackinit/nginx-brotli
```

For extra information, please refer to the [official Docker Hub Nginx documentation](https://hub.docker.com/_/nginx/), since this image builds upon it.

In addition, you can look for Brotli configurations at the upstream repository [eustas/ngx_brotli](https://github.com/eustas/ngx_brotli#configuration-directives).


## Sample config

To enable TLS 1.3, add:

```nginx
ssl_protocols TLSv1.2 TLSv1.3;
ssl_ciphers [TLS13+AESGCM+AES128|TLS13+AESGCM+AES256|TLS13+CHACHA20]:[EECDH+ECDSA+AESGCM+AES128|EECDH+ECDSA+CHACHA20]:EECDH+ECDSA+AESGCM+AES256:EECDH+ECDSA+AES128+SHA:EECDH+ECDSA+AES256+SHA:[EECDH+aRSA+AESGCM+AES128|EECDH+aRSA+CHACHA20]:EECDH+aRSA+AESGCM+AES256:EECDH+aRSA+AES128+SHA:EECDH+aRSA+AES256+SHA:RSA+AES128+SHA:RSA+AES256+SHA:RSA+3DES;
```

To enable Brotli, add this in `http` block:

```nginx
brotli on;  
brotli_comp_level 6;  
brotli_buffers 16 8k;  
brotli_min_length 20;  
brotli_types *;
```

## Modification Details

Module [ngx_brotli](https://github.com/eustas/ngx_brotli) has been added for Brotli support.

## Manually build from source

```bash
git clone git://github.com/hackinit/docker-nginx.git
cd docker-nginx
docker build -t nginx-brotli:latest .
```
