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


docker run -d --expose 80 --expose 443 --name schoolhub_api_gateway  -e "VIRTUAL_HOST=api.schoolhubb.com" -e "LETSENCRYPT_HOST=api.schoolhubb.com" -e "LETSENCRYPT_EMAIL=api@schoolhubb.com" cyberadvance/schoolhub-api-gateway
