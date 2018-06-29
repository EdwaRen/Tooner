# Tooner
Tooner includes the entire stack necessary to set-up our production Nginx server with full SSL/HTTPS encryption.

Everything is dockerized in a Docker container for quick, portable setup on any server.

## Certbot
Certbot is necessary for enabling SSL on our Nginx server. A cron job renews our certificate automatically near the expiration date.


### Generate certificate:

```
sudo docker run -it --rm \
-v /docker-volumes/etc/letsencrypt:/etc/letsencrypt \
-v /docker-volumes/var/lib/letsencrypt:/var/lib/letsencrypt \
-v /docker/letsencrypt-docker-nginx/src/letsencrypt/letsencrypt-site:/data/letsencrypt \
-v "/docker-volumes/var/log/letsencrypt:/var/log/letsencrypt" \
certbot/certbot \
certonly --webroot \
--register-unsafely-without-email --agree-tos \
--webroot-path=/data/letsencrypt \
--staging \
-d landlorater.ml -d www.landlorater.ml
```

### Check Certificate is working
```
sudo docker run --rm -it --name certbot \
-v /docker-volumes/etc/letsencrypt:/etc/letsencrypt \
-v /docker-volumes/var/lib/letsencrypt:/var/lib/letsencrypt \
-v /docker/letsencrypt-docker-nginx/src/letsencrypt/letsencrypt-site:/data/letsencrypt \
certbot/certbot \
--staging \
certificates
```
