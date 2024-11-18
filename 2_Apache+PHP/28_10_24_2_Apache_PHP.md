# **Running a PHP webpage with Apache Server using Docker Compose**

**Introduction**

Docker Compose is a powerful tool that allows you to define and run multi-container Docker applications. In this guide, we'll demonstrate how to set up a simple web application using an Apache server, all managed by Docker Compose.

**Prerequisites:**

* **Docker:** Ensure Docker is installed and running on your system.
* **Docker Compose:** Install Docker Compose, often bundled with Docker Desktop or available via package managers.

**Steps:**

## 1. Downloading Docker Desktop on Windows

**1. Go to the Docker Desktop Download Page:**

* Visit the official Docker Desktop download page: https://www.docker.com/products/docker-desktop/



**2. Download the Installer:**

* Click the **Download for Windows** button.
* Save the downloaded installer file (usually a `.exe` file) to your computer.

**3. Run the Installer:**

* Double-click the downloaded installer file to start the installation process.
* Follow the on-screen instructions to complete the installation.

**4. Start Docker Desktop:**

* Once the installation is complete, Docker Desktop will start automatically.
* You can also start it manually from the Start menu.

## 2. Setting Up Apache Server with Docker Compose

This guide will help you set up an Apache server using Docker Compose.


## Step 1: Create a Project Directory

Create a directory for your project:

Name the file as your wish

- Docker_file
  - 1_Apache_Game
    - docker-compose.yml
    - src
      - index.php
    ### After then paste this code in docker-compose.yml


```yml
services:
  web:
    image: php:8.1-apache
    ports:
      - "8081:80"
    volumes:
      - ./src:/var/www/html
    restart: always

```
---

Then Compose Up 

Then a new file called **src** will be created Automatically

open the **src** file and paste your web page in the file

```PHP
<?php
echo("Hello World");
echo("This is on port 8081");
?>


  ```
## Then open any Browser Search for 

# **localhost:8081**
  



