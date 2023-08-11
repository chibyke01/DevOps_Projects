# LAMP STACK IMPLEMENTATION

This project outlines the implementation process of a LAMP (Linux, Apache, MySQL, PHP) Stack on Linux-based server. It provides step-by-step instructions with screenshots from my Lab for installing and configuring each component of the stack, along with basic security considerations.

**LAMP stack** is an open-source software bundle used to build websites and web applications. LAMP is an acronym that consist of these four main components/operating system:

* **L - Linux**: The operating system that provides the foundation for the stack.
* **A - Apache**: A web server(HTTP Server) software that serves web content to users.
* **M - MySQL**: A relational database management system used to store and manage data.
* **P - PHP**: A server-side scripting language used to build dynamic web pages and applications.

LAMP stacks is used to create, host, and maintain web content. It is a popular solution that powers many of the websites that is commonly used today.

**Prequisites**:
-
* A Cloud provider Instance (AWS EC2)
* Linux distribution (e.g., Ubuntu Server)
* Root or sudo access to the server.

To start this project I inatall an OpenSSH on my windows machine using the below link:
[OpenSSH for Windows](https://learn.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse?tabs=powershell#install-openssh-for-windows)

Created an instance using my AWS EC2

Connect to EC2 instance via ssh using my Terminal:
* cd Downloads (where my .pem file is located)
* ssh -i <private-key-name>.pem ubuntu@<Public-IP-address>
![Alt text](image.png)

# Installing Apache And Updating the Firewall
update a list of packages in package manager and run apache package installation.

`sudo apt update` 
`sudo apt install apache2`

To confirm service was running successfuly run the below cmd and if it is Green and running this confirms that the installation was done correctly.
`sudo systemctl status apache2`

![Alt text](image-2.png)

Open Port 80 on my EC2 server as this is the default port a web browser use to access web pages.
![Alt text](image-3.png)

Run the curl cmd: as this is used to request Apache HTTP Server on open port 80. 
`curl http://localhost:80`
`curl http://127.0.0.1:80`

With this the Apache installation is complete and for confirmation, run the below cmds to view your webpage:
`http://<Public-IP-Address>`
`http://<Public-IP-Address>:80`

N/B - You can also get the Public IP using running the below cmd on your terminal:
`curl -s http://169.254.169.254/latest/meta-data/public-ipv4`

On your web browser type **http://<Public-IP-Address>:80** if the below default page output is what you get then it confirms that the web server is installed correctly and can be accessed through port 80.
![Alt text](image-4.png)

## Installing MySQL Database
To start the installion of mysql-server run the below and when prompted confirm installation by typing Y:
$ sudo apt install mysql-server

Run the below cmds to connect to MYSQL server administractve database:
$ sudo mysql
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';
$ mysql> exit

To start intractive scripting.
 sudo mysql_secure_installation

After the steps above to confirm the installation login to confirm installation and exist:
`mysql -p`
`mysql> exit`
![Alt text](image-5.png)























