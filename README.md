# Docker Nginx

Dockerized Nginx with TLS 1.3 and Brotli support.

Based on [nginxinc/docker-nginx](https://github.com/nginxinc/docker-nginx).

## Config

To enable TLS 1.3, use:

```nginx
ssl_protocols TLSv1.1 TLSv1.2 TLSv1.3;
ssl_ciphers [TLS13+AESGCM+AES128|TLS13+AESGCM+AES256|TLS13+CHACHA20]:[EECDH+ECDSA+AESGCM+AES128|EECDH+ECDSA+CHACHA20]:EECDH+ECDSA+AESGCM+AES256:EECDH+ECDSA+AES128+SHA:EECDH+ECDSA+AES256+SHA:[EECDH+aRSA+AESGCM+AES128|EECDH+aRSA+CHACHA20]:EECDH+aRSA+AESGCM+AES256:EECDH+aRSA+AES128+SHA:EECDH+aRSA+AES256+SHA:RSA+AES128+SHA:RSA+AES256+SHA:RSA+3DES;
```
To enable Brotli, use this in `http` block:

```nginx
brotli on;  
brotli_comp_level 6;  
brotli_buffers 16 8k;  
brotli_min_length 20;  
brotli_types *;
```

## Modification Details

Compiled with patched OpenSSL 1.1.1b, supports TLS 1.3 draft 23, 26, 28 and final.

Module [ngx_brotli](https://github.com/google/ngx_brotli) has been added for Brotli support.

## Build

```bash
git clone git://github.com/hackinit/docker-nginx.git
cd docker-nginx
docker build -t nginx:1.15.11-modified .
```