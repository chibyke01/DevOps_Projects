# ANSIBLE CONFIGURATION MANAGEMENT
Ansible is an open source IT automation tool that automates provisioning, configuration management, application deployment, orchestration, and many other manual IT processes. Unlike more simplistic management tools, Ansible can be used to automate software inatallation, automate daily tasks, provision infrastructure, improve security and compliance, patch systems, and share automation across the entire organization.

In this project Ansible Client act as a **Jump Server**(sometimes referred to as Bastion Host), **Jump Server** is an intermediary server through which access to internal network can be provided. In this project architecture the webservers will be inside a secured network which cannot be reached directly from the internet, this means that the webservers can only be accessed through the **Jump Server**, this set up provides better security and reduces attack.

The diagram below is a typical description of that explains a **Jump server/Bastion Host**, the Virtual Private Network (VPC) is divided into two subnets, the Public subset which has a public IP addresses and the Private Subset that is only reachable or accessed by Private IP addresses from the Bastion Host.
![Alt text](Images/Diagram.png)

## Install and Configure Jenkins and Ansible on EC2 instance
* Install Jenkins on ec2 instance using the below commands
```
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
    /usr/share/keyrings/jenkins-keyring.asc > /dev/null

echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
    https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
    /etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt-get update
sudo apt-get install fontconfig openjdk-11-jre
sudo apt-get install jenkins
```
* Install ansible using the below commands
```
sudo apt update
sudo apt install ansible

```
Confirm that ansible is installed on the terminal by confirming the version with **ansible --version** 
![Alt text](<Images/Confirmed my ansible was installed correctly.png>)

To confirm that Jenkins was installed correctly run **sudo systemctl status jenkins**
![Alt text](<Images/Jenkins is up and running.png>)

In other to configure Jenkins, we need to note that jenkins listens to port 8080 by default, however we use the public ip of the instance where jenkins is installed and the port it listens to, the port will be opened on the security group of the instance. The below diagram confirms a complete Jenkins set up.
![Alt text](<Images/Jenkins successful setup.png>)

