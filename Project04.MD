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
![Image](image-12.png)

How to access it locally from ubuntu

`curl http://localhost:80`

`curl http://100.24.5.4:80`


On the web browser I used the below to view the NGINX page and to confirm set up.

`http://100.24.5.4:80`
![Alt text](image-13.png)








