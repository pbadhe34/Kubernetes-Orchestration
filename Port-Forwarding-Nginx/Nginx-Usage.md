docker build -t my-nginx .

docker-compose up -d

Test it with urls as

http://localhost:8080  : NGinx server

http://localhost:9080  : Apachge Server


http://localhost:9090  : Py-app 


docker run -p 8080:80 -p 8070:8070--name nginx -d my-nginx

docker run -p 8070:8070 --name nginx -d my-nginx


docker ps --format "{{.ID}}: {{.Image}} {{.Names}}"

nginxproxy:
    image: my-nginx
    ports:
         - 8080:80
         - 8070:8070
    restart: always
