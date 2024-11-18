# **Docker Compose for Apache, PHP, and MySQL**


## Step 1: Create a Project Directory

Create a directory for your project:

Name the file as your wish

- Docker_file
  - 3_Apache_PHP_mysql
    - docker-compose.yml
    - Dockerfile

   ![alt text](<31.1.png>) 

    ### After then paste this code in docker-compose.yml And *Compose up*


```yml
services:
  php:
    build:
      context: .
      dockerfile: Dockerfile
    volumes:
      - ./src:/var/www/html
    ports:
      - "8080:80"
    depends_on:
      - mysql

  mysql:
    image: mysql:5.7
    environment:
      MYSQL_ROOT_PASSWORD: root_password
      MYSQL_DATABASE: my_database
      MYSQL_USER: user
      MYSQL_PASSWORD: user_password
    ports:
      - "3306:3306"
    volumes:
      - mysql_data:/var/lib/mysql

volumes:
  mysql_data:

```
---
![Pasting the code](<3.1.png>)

### After then paste this code in Dockerfile

```docker

FROM php:8.0-apache

RUN docker-php-ext-install mysqli

```

![Pasting the code](<3.2.png>)

Then a new file called **src** will be created Automatically

![alt text](<3.5.png>) 

## Open the *src* file and create a *index.php* and *add_user.php*

- Docker_file
  - 3_Apache_PHP_mysql
    - docker-compose.yml
    - Dockerfile
    - src
        - index.php
        - add_user.php



```PHP
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>User Registration</title>
    
</head>
<body>
    <h1>Add User</h1>
    <form action="add_user.php" method="post">
        <input type="text" name="username" placeholder="Username" required>
        <input type="password" name="password" placeholder="Password" required>
        <input type="submit" value="Add User">
    </form>
    <style>
body {
    font-family: Arial, sans-serif;
    background-color: #f4f4f4;
    margin: 0;
    padding: 20px;
}

h1 {
    color: #333;
}

form {
    background: #fff;
    padding: 20px;
    border-radius: 5px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    max-width: 400px;
    margin: auto;
}

input[type="text"],
input[type="password"] {
    width: 100%;
    padding: 10px;
    margin: 10px 0;
    border: 1px solid #ccc;
    border-radius: 5px;
}

input[type="submit"] {
    background: #5cb85c;
    color: white;
    border: none;
    padding: 10px;
    border-radius: 5px;
    cursor: pointer;
    width: 100%;
}

input[type="submit"]:hover {
    background: #4cae4c;
}

        </style>
</body>
</html>
<?php
$servername = "mysql"; // MySQL service name in docker-compose.yml
$username = "user";     // Username
$password = "user_password"; // User password
$dbname = "Naseer_database"; // Name of the database you created

// Create connection
$conn = new mysqli($servername, $username, $password, $dbname);

// Check connection
if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}

// Example query: Fetch users from the database
$sql = "SELECT * FROM users";
$result = $conn->query($sql);

if ($result->num_rows > 0) {
    // Output data of each row
    while($row = $result->fetch_assoc()) {
        echo "id: " . $row["id"] . " - Username: " . $row["username"] . "<br>";
    }
} else {
    echo "0 results";
}

$conn->close();
?>

  ```
  ---
![index.php](<3.3.png>)

```php

<?php
$servername = "mysql"; // MySQL service name
$username = "user";     // MySQL username
$password = "user_password"; // MySQL password
$dbname = "Naseer_database"; // Your database name

// Create connection
$conn = new mysqli($servername, $username, $password, $dbname);

// Check connection
if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}

// Get the form data
$user = $_POST['username'];
$pass = $_POST['password'];

// Prepare and bind
$stmt = $conn->prepare("INSERT INTO users (username, password) VALUES (?, ?)");
$stmt->bind_param("ss", $user, $pass);

// Execute the statement
if ($stmt->execute()) {
    echo "New user added successfully.";
} else {
    echo "Error: " . $stmt->error;
}

// Close the connection
$stmt->close();
$conn->close();
?>
```
---
![add_user.php](<3.4.png>)


You can access the terminal by using this code

```bash

$ docker exec -it mysql-container mysql -u root -p
Enter password:root_password

```
Then create the DataBase and table
```mysql

mysql> CREATE DATABASE Naseer_database;
mysql> USE Naseer_database;
mysql> CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    password VARCHAR(100),
);


```

## Then open any Browser Search for 

# **localhost:8080**
  
![alt text](<3.6.png>) 
