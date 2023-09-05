# LEMP STACK IMPLEMENTATION
The LEMP stack is a combination of four open-source technologies that are used in web development. These technologies include:

* **Linux:** The operating system that runs the web server.
* **Nginx:** The web server software that handles HTTP requests, Nginx *(pronounced as **engine-x**, hence the **E** in the acronym)*.
* **MySQL:** The relational database management system that stores the website’s data.
* **PHP:** The programming language used to build dynamic web applications.

The LEMP stack works by using Nginx as the web server, which listens for HTTP requests and forwards them to the appropriate PHP script. The PHP script generates a response, which is then sent back to the user via Nginx.
MySQL is used to store and manage the website’s data. PHP communicates with MySQL to retrieve and store data as needed.

First I ssh into my EC2 instance using git bash terminal and opened post:80 as my default web browser access.

## Installing NGINX
Updating my server package and installing NGINX

`sudo apt update`

`sudo apt install nginx`


To verify NGINX installed correctly and open port:80 as default
 
`sudo systemctl status nginx`
![image](https://github.com/chibyke01/DevOps_Projects/assets/103823637/cb3957a8-cf79-42d4-9980-01d7b3a04acc)

How to access it locally from ubuntu

`curl http://localhost:80`

`curl http://100.24.5.4:80`


On the web browser I used the below to view the **NGINX** page and to confirm set up.

`http://100.24.5.4:80`

![image](https://github.com/chibyke01/DevOps_Projects/assets/103823637/44bb4aa0-c03e-4df5-b920-2d65ddc82315)

## Installing MySQL
To install run

sudo apt install mysql-server

Login to MySQL and set the password

`sudo mysql`

`ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';`

`mysql> exit`

To start the interactive scripting to validate password **(type password on prompt)**, sign in to MySQL and exit
```
sudo mysql_secure_installation
sudo mysql -p
mysql> exit
```

## Installing PHP

Run the below cmd to install Php on the server

`sudo apt install php-fpm php-mysql`

## Configure NGINX to use PHP processor.
On Ubuntu 20.04, Nginx has one server block enabled by default and is configured to serve documents out of a directory at **/var/www/html**, while this works for a single site, it can become difficul if you try to host mutiple sites, however insted of modifying **/var/www/html**, will create a directory for the domain and leaving the default directory should incase we could not match any client fails to match with the any site.

`sudo mkdir /var/www/projectLEMP`

Assign ownership of the variables, user environment

`sudo chown -R $USER:$USER /var/www/projectLEMP`

Open a configuration file


`sudo nano /etc/nginx/sites-available/projectLEMP`

```
#/etc/nginx/sites-available/projectLEMP

server {
    listen 80;
    server_name projectLEMP www.projectLEMP;
    root /var/www/projectLEMP;

    index index.html index.htm index.php;

    location / {
        try_files $uri $uri/ =404;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php8.1-fpm.sock;
     }

    location ~ /\.ht {
        deny all;
    }

}
```
Activating the configuration and linking the config file to NGINX

`sudo ln -s /etc/nginx/sites-available/projectLEMP /etc/nginx/sites-enabled/`

Check for errors

`sudo nginx -t`

![image](https://github.com/chibyke01/DevOps_Projects/assets/103823637/46f9ac55-1bc2-425c-8c5e-fc947455de2b)


Disable the default NIGINX that is configured to host 80, reload NIGINX to save the changes and add content to the .html file using touch and vi editor.
```
sudo unlink /etc/nginx/sites-enabled/default

cd /var/www/projectLEMP

touch index.html

vi index.html
```
![image](https://github.com/chibyke01/DevOps_Projects/assets/103823637/98b1c2fa-f048-4879-9fed-f23b34e16bdf)

Type the below on a browser to confirm our webpage.

`http://<Public-IP-Address>:80`

![image](https://github.com/chibyke01/DevOps_Projects/assets/103823637/4ffc9372-a38c-4a50-975c-c9ea78b3e24e)

## Testing PHP with NGINX
However at this point the LEMP has been set up, but we need to validate that the NGINX can correctly hand .php file to PHP processor.

Create a file in the document root
Open the file in vi editor and paste the **info**
```
cd /var/www/projectLEMP

touch info.php

vi /var/www/projectLEMP/info.php

<?php
phpinfo();
```
Type the below address on the web browser

`http://<Public.IP/info.php`

![image](https://github.com/chibyke01/DevOps_Projects/assets/103823637/54d71cb9-9ec7-48d5-9e60-ba7469d09c7e)


## Retrieving data from MySQL database with PHP

Connect to MySQL

`sudo mysql`

Create a database and a user

```
mysql> CREATE DATABASE `example_database`;

mysql>  CREATE USER 'example_user'@'%' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';
```

Give the user permission over the database and exit

```
mysql> GRANT ALL ON example_database.* TO 'example_user'@'%';

mysql> exit
```

Check if the user has the given permission
```
mysql -u example_user -p

mysql> SHOW DATABASES;
```
Create a table nameed Todo_list and insert some rows of contents
```
CREATE TABLE example_database.todo_list (item_id INT AUTO_INCREMENT,content VARCHAR(255),PRIMARY KEY(item_id));

mysql> INSERT INTO example_database.todo_list (content) VALUES ("My first important item");
```
Confirm that it was saved by running the below cmd and exit MySQL

`mysql>  SELECT * FROM example_database.todo_list;`

`mysql> exit`

![image](https://github.com/chibyke01/DevOps_Projects/assets/103823637/31a17d60-d4c4-4c66-846d-64ea0a1c7286)

Create a php in the root directory using any editor of choice

`vi /var/www/projectLEMP/todo_list.php`

Paste the below script, save and exit **(:wq + enter)**
```
<?php
$user = "example_user";
$password = "PassWord.1";
$database = "example_database";
$table = "todo_list";

try {
  $db = new PDO("mysql:host=localhost;dbname=$database", $user, $password);
  echo "<h2>TODO</h2><ol>";
  foreach($db->query("SELECT content FROM $table") as $row) {
    echo "<li>" . $row['content'] . "</li>";
  }
  echo "</ol>";
} catch (PDOException $e) {
    print "Error!: " . $e->getMessage() . "<br/>";
    die();
}
```

Type the below in the webpage

`http://<Public_domain_or_IP>/todo_list.php`

![image](https://github.com/chibyke01/DevOps_Projects/assets/103823637/331db564-55ad-4cc1-a49d-feac8b4fd756)





_**Thank you**_




