# schoolhub-api-gateway
วิธีการ Deploy HTTPS

docker run -d -p 80:80 -p 443:443 --name nginx-proxy \
-v /server/path/certs:/etc/nginx/certs:ro \
-v /etc/nginx/vhost.d \
-v /usr/share/nginx/html \
-v /var/run/docker.sock:/tmp/docker.sock:ro \
jwilder/nginx-proxy



docker run -d --name ssl-auto-gen \
-v /server/path/certs:/etc/nginx/certs:rw \
--volumes-from nginx-proxy \
-v /var/run/docker.sock:/var/run/docker.sock:ro \
jrcs/letsencrypt-nginx-proxy-companion


docker run -d --expose 80 --expose 443 --name casan_service_gateway  -e "VIRTUAL_HOST=casan-sevice.lamunphan.com" -e "LETSENCRYPT_HOST=casan-sevice.lamunphan.com" -e "LETSENCRYPT_EMAIL=casan@lamunphan.com" cyberadvance/casan-service-gateway
