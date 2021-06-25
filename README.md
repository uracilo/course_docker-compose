# course_docker-compose

## Version

```bash
version: '2'
```
## First Service database

```bash
services:
  mysql:
    image: mysql:5.7
    restart: always
    ports:
      - 8081:3306
    environment:
      MYSQL_USER: wordpress
      MYSQL_ROOT_PASSWORD: wordpress
      MYSQL_DATABASE: wordpress
      MYSQL_PASSWORD: wordpress
    networks:
      - backend
```
## Second service Wordpress

```bash
  wordpress:
    depends_on:
      - mysql
    image: wordpress
    ports:
      - 8080:80
    restart: always
    volumes:
      - ./:/var/www/html/wp-content/plugins/nelio-content
    environment:
      VIRTUAL_HOST: content.local
      VIRTUAL_PORT: 8080
      WORDPRESS_DB_HOST: mysql:3306
      WORDPRESS_DB_USER: wordpress
      WORDPRESS_DB_PASSWORD: wordpress
    networks:
      - frontend
      - backend
```

## Network

```bash
networks:
  backend:
  frontend:
    external:
      name: proxy
```

