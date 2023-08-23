# IMPLEMENTING LOAD BALANCER WITH NGINX WEBSEVER

## Introduction to Load Balancer
In this project I will learn how to distribute traffic efficiently accross mutiple servers, optimise performance and ensure high availability for a web application

![Alt text](image.png)
         **Load Balancer System Diagram**

The above diagram gives a pictorial definition of a load balancer, which can also be defined as a Device or application that distributes network and/or application traffic accross multiple servers or applications. 

This helps to optimise the use of computing resource, increases the capacity and reliability of applications and prevent network overload.

A load balancer can act like a reverse proxy and can be hardware or virtual machine.

## Setting up a Load Balancer
Create two(2) EC2 VM with Ubuntu server 20.04 LTS and named them ecs-nginx-server and ec2-apache2-server.

On the apache2 ec2 instance, created an inbound rule to allow traffic/listen to port 8000.
![Alt text](image-1.png)

Updated the remotely connected SSH EC2 instance and installed apache2 web sever on the terminal.
```
sudo apt update 
sudo apt upgrade 
sudo apt update -y &&  sudo apt install apache2 -y
```
![Alt text](image-2.png)

Confirmed installation was successfull by checking the status.
`sudo systemctl status apache2`

![Alt text](image-3.png)

To confirgure the Apache2 to listen to port 8000 as allowed on my instance I need to edit the port.conf file, the 000-default.conf file.

For the port.conf file, added Listen 8000, used :wq! to save and exit vi editor.

`sudo vi /etc/apache2/ports.conf`

![Alt text](image-5.png)
![Alt text](image-4.png)

For the 000-default.conf file changed the default Virtual Host to 8000.

`sudo vi /etc/apache2/sites-available/000-default.conf`

![Alt text](image-6.png)
![Alt text](image-7.png)

To use a customised web page, edit the default index.html file of Apache webserver, using **:1,$d** - to highlight and delete all content of the default webserver paste a customised web page code, save and exit **:wq!**.

`vi /var/www/index.html`
```
        <!DOCTYPE html>
        <html>
        <head>
            <title>WELCOME TO CHIBUIKE EC2 INSTANCE</title>
        </head>
        <body>
            <h1>My name is CHIBUIKE NWOSU, In this project I configured the Apache2 webserver to listen on port 8000 </h1>
            <p>Public IP: YOUR_PUBLIC_IP</p>
        </body>
        </html>
```