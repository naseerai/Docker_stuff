# Running WordPress with Docker

## Prerequisites
- Docker installed on your machine
- Docker Compose installed

## Step 1: Create a Project Directory

Create a directory for your project:

Name the file as your wish

- Docker_file
  - 4_
    - docker-compose.yml

After creating `docker-compose.yml` and add the following content:

```yaml

services:
  db:
    image: mysql:5.7
    container_name: mysql_db
    restart: always
    environment:
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wordpress_user
      MYSQL_PASSWORD: wordpress_password
      MYSQL_ROOT_PASSWORD: root_password
    volumes:
      - db_data:/var/lib/mysql

  wordpress:
    image: wordpress:latest
    container_name: wordpress_site
    depends_on:
      - db
    ports:
      - "8082:80"
    restart: always
    environment:
      WORDPRESS_DB_HOST: db:3306
      WORDPRESS_DB_NAME: wordpress
      WORDPRESS_DB_USER: wordpress_user
      WORDPRESS_DB_PASSWORD: wordpress_password
    volumes:
      - wordpress_data:/var/www/html

volumes:
  db_data:
  wordpress_data:


```
---
