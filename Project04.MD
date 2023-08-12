# LEMP STACK IMPLEMENTATION
The LEMP stack is a combination of four open-source technologies that are used in web development. These technologies include:

* **Linux:** The operating system that runs the web server.
* **Nginx:** The web server software that handles HTTP requests, Nginx *(pronounced as **engine-x**, hence the **E** in the acronym)*.
* **MySQL:** The relational database management system that stores the website’s data.
* **PHP:** The programming language used to build dynamic web applications.

The LEMP stack works by using Nginx as the web server, which listens for HTTP requests and forwards them to the appropriate PHP script. The PHP script generates a response, which is then sent back to the user via Nginx.
MySQL is used to store and manage the website’s data. PHP communicates with MySQL to retrieve and store data as needed.

First I ssh into your EC2 instance using git bash terminal and opened post:80 as my default web browser access.

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











