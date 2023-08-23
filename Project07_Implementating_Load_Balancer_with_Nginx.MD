# IMPLEMENTING LOAD BALANCER WITH NGINX WEBSEVER

## Introduction to Load Balancer
In this project will learn how to distribute traffic efficiently accross mutiple servers, optimise performance and ensure high availability for a web application

![image](https://github.com/chibyke01/DevOps_Projects/assets/103823637/4b8d279a-e975-4a61-ba3b-e6cc3c2128de)
         **Load Balancer System Diagram**

The above diagram gives a pictorial definition of a load balancer, which can also be defined as a Device or application that distributes network and/or application traffic accross multiple servers or applications. 

This helps to optimise the use of computing resource, increases the capacity and reliability of applications and prevent network overload.

A load balancer can act like a reverse proxy and can be hardware or virtual machine.

## Setting up a Load Balancer
Create two(2) EC2 VM with Ubuntu server 20.04 LTS and named them ecs-nginx-server and ec2-apache2-server.

**Apache2 Webserver Configuration**

1. On the apache2 ec2 instance, created an inbound rule to allow traffic/listen to port 8000.
![image](https://github.com/chibyke01/DevOps_Projects/assets/103823637/e30958db-7b2a-4ce2-b439-e7f258d76328)

2. Update the remotely connected SSH EC2 instance and installed apache2 web sever on the terminal.
```
sudo apt update 
sudo apt upgrade 
sudo apt update -y &&  sudo apt install apache2 -y
```
![image](https://github.com/chibyke01/DevOps_Projects/assets/103823637/b31c5e17-23fc-47a4-a4b3-088d6c50fe86)

* Confirmed installation was successfull by checking the status.
`sudo systemctl status apache2`

![image](https://github.com/chibyke01/DevOps_Projects/assets/103823637/70080f48-876f-4eeb-9d9f-81afd948b261)

3. Confirgure the Apache2 to listen to port 8000 as allowed on my instance I need to edit the **port.conf** file, the **000-default.conf** file.

* For the port.conf file, added Listen 8000, used :wq! to save and exit vi editor.

`sudo vi /etc/apache2/ports.conf`

![image](https://github.com/chibyke01/DevOps_Projects/assets/103823637/6d1dd8bc-9834-438e-ae87-18d78c8069b5)
![image](https://github.com/chibyke01/DevOps_Projects/assets/103823637/95fe42f3-ce28-42e8-95ef-fae1fe1bd092)

* For 000-default.conf file changed the default Virtual Host to 8000.

`sudo vi /etc/apache2/sites-available/000-default.conf`

![image](https://github.com/chibyke01/DevOps_Projects/assets/103823637/c5e6598b-db49-4c5d-b71e-b3b9d8ebb823)
![image](https://github.com/chibyke01/DevOps_Projects/assets/103823637/48a723f9-0347-4035-945a-85cb2f830745)

4. Customise the web page by editing the default index.html file of Apache webserver, using **:1,$d** - to highlight and delete all content of the default webserver paste a customised web page code, save and exit **:wq!**.

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
* Run the below cmd as this will restart the server and update the changes/configurations.

`sudo systemctl restart apache2`

At this point we have successufully completed the apache2 webserver set up, to test we need to use the public IP and the port.

`54.225.11.151:8000`

![image](https://github.com/chibyke01/DevOps_Projects/assets/103823637/136517b6-2a3c-42d9-8941-915e73eef83a)

-----

**Nginx Load Balancer Configuration**

1. Set up http inbound rule and open port 6000 on the AWS instance.

![image](https://github.com/chibyke01/DevOps_Projects/assets/103823637/94f85cb4-4d18-4569-bd6f-538551266b0e)

2. SSH remotely to EC2 instance, update, upgrade and install the nginx webserver.
```
sudo apt install update 
sudo apt install upgrade 
sudo apt update -y && sudo apt install nginx -y
```
* Confirm if the installation was successful by running the below cmd.

`sudo systemctl status nginx`

3. Open nginx configuration file.

`sudo vi /etc/nginx/conf.d/loadbalancer.conf`

 * Paste the below configuration file that will enable the nginx webserver to act as a Load balancer.
```
        upstream backend_servers {

            # your are to replace the public IP and Port to that of your webservers
            server 54.152.206.183:8000; # public IP and port for webserser 1
            server 52.91.209.178:6000; # public IP and port for webserver 2

        }

        server {
            listen 80;
            server_name 52.91.209.178; # provide your load balancers public IP address

            location / {
                proxy_pass http://backend_servers;
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            }
        }
```
* **N/B** This confirguration is not static as the public IP address are from my AWS instance, this can be changed to suit your configuration.

* Test my nginx configuration to congirm if its successful.

`sudo nginx -t`

![image](https://github.com/chibyke01/DevOps_Projects/assets/103823637/1a9e5399-ff71-4172-beb9-6566baae2da7)

* Restart nginx server to allow for the configurations to take effect.

`sudo systemctl restart nginx`

At this point we are fine with the setup/configuration for the nginx server to act as a Load balancer, however to prove the success of this configuration I will use the nginx public ip to make a request to the apache2 webserver, the result/output will be the configuration on set up on my apache2 server.
 
The request will done using the publis IP of the apache2 and nginx web server to see if it will give us same result.

* Public IP Nginx server (Load Balancer)
![image](https://github.com/chibyke01/DevOps_Projects/assets/103823637/70924aad-fbb2-4433-b2f4-6cb18de481b6)

* Public IP Apache2
![image](https://github.com/chibyke01/DevOps_Projects/assets/103823637/c4b2b8cc-869c-4215-8705-ae7d6e189259)

* Web page request using nginx and apache2 public IP.
![image](https://github.com/chibyke01/DevOps_Projects/assets/103823637/373a9c97-8634-4819-b9a6-5f343e97ea3d)



## _Thank You_
