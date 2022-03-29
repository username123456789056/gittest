# gittest
version: '3'

services:
  product-service:
   build: ./nodedockerweb
   volumes:
    - ./nodedockerweb:/usr/src/app
   ports:
    - 3000:3000
   
   
   
  web-test:
   image: "nginx:latest" 
   
   
  web-test1:
   image: "kodekloud/simple-webapp:latest"
   
    
  db:
    image: mysql:5.7
    volumes:
      - db_data:/var/lib/mysql
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: somewordpress
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wordpress
      MYSQL_PASSWORD: wordpress
    
  wordpress:
    depends_on:
      - db
    image: wordpress:latest
    volumes:
      - wordpress_data:/var/www/html
    ports:
      - "8000:80"
    restart: always
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: wordpress
      WORDPRESS_DB_PASSWORD: wordpress
      WORDPRESS_DB_NAME: wordpress
volumes:
  db_data: {}
  wordpress_data: {}
