# CLIENT SERVER ARCHITECTURE WITH MYSQL AS RDBMS
Client server refers to an architecture in which two or more computers are connected together over a network to send and receive request between one another.
* Client - Refers to the machine sending the request
* Server - Refers to the machine responding to the request.

## Prerequisite
* Two(2) AWS EC2 instance(Ubuntu)
* Windows Powershell 

In other to implement this project, I will start by creating two(2) EC2 instances in AWS and named each of the instances as seen below and connected it to the windows powershell terminal remotely:
```
Server 1 name - MySQL Server
Server 2 name - MySQL Client 
```
On both terminals, first I ran the sudo update and upgrade cmds to update my packages.
```
sudo apt update 
sudo apt upgrade
```
![image](https://github.com/chibyke01/DevOps_Projects/assets/103823637/fdc892cc-d3b4-48af-89a9-747747aec5d5)

After successfuly update and upgrade, I Installed Mysql-server on both the Mysql client and Mysql server terminals using the below cmds

`sudo apt install mysql-server`

![image](https://github.com/chibyke01/DevOps_Projects/assets/103823637/0726f77a-3c4f-4007-a513-0c2480c1853c)
![image](https://github.com/chibyke01/DevOps_Projects/assets/103823637/c71dbcf0-9cf5-4135-978d-bb5927e35468)

Set up password authentication/native password methods for mysql and remove any insecure default settings I ran the below cmds on both client and sever.

`$ sudo mysql`

Set up a password using the below cmds.

`ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'Chibyke.1';`

`mysql> exit`
![image](https://github.com/chibyke01/DevOps_Projects/assets/103823637/e7229a20-2f45-40b6-a624-2f56023ed124)

Ran the password validation cmd, and choosed the medium setting (1), this validation is also to enable password strength criteria.

`$ sudo mysql_secure_installation`

At this point since we have mysql-server installed on both servers(MySQL_Client and MySQL_Server), we need to connect both host remotely, but before we do this they are still some configurations required to allow for remote connections.

On the EC2 instance for MySQL_Server(configuration will be done on this seever since we are using the client to connect remotely) we need to open TCP port 3306, as that is the port MySQL server listens to by default, this is do done by creating an inbound rule.

![image](https://github.com/chibyke01/DevOps_Projects/assets/103823637/ae8711a4-20b9-4d5f-aa62-7b1239c5974d)

I also configured MySQL server to allow for connections by using the vi editor to locate the below file path.

`sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf`

On the vi editor I replaced the **127.0.0.1 to 0.0.0.0** on the **bind-address = 0.0.0.0.**, I also commented it out, used **:wq!** to save and exit the vi editor.

Ran the below cmd to reload and confirm the status of the both servers to know if they are actively running.
```
sudo systemctl restart mysql.service
sudo systemctl status mysql.service
```
With the above successfully set up we are now ready to connect remotely from the MySQL_Client server, connected using the below cmd.

`mysql -u root -p --port 3306`

![image](https://github.com/chibyke01/DevOps_Projects/assets/103823637/e9cb8805-649d-41b7-959c-b2b08a3feb32)


## **_Thank you_**























