


script to automate the Apache2 server

```
#!/bin/bash

####################################################################################################################
##### This automates the installation and configuring of apache webserver to listen on port 8000
##### Usage: Call the script and pass in the Public_IP of your EC2 instance as the first argument as shown below:
######## ./install_configure_apache.sh 127.0.0.1
####################################################################################################################

set -x # debug mode
set -e # exit the script if there is an error
set -o pipefail # exit the script when there is a pipe failure

PUBLIC_IP=$1

[ -z "${PUBLIC_IP}" ] && echo "Please pass the public IP of your EC3 instance as an argument to the script" && exit 1

sudo apt update -y && sudo apt install apache2 -y

# Ensure Apache service is running
sudo systemctl start apache2

if [[ $? -eq 0 ]]; then
    # Change permissions for necessary files and directories
    sudo chmod 777 /etc/apache2/ports.conf
    sudo chmod 777 -R /etc/apache2/
    sudo chmod 777 -R /var/www/html/

    # Update VirtualHost configuration
    sudo sed -i 's/<VirtualHost \*:80>/<VirtualHost *:8000>/' /etc/apache2/sites-available/000-default.conf

    # Create and configure the index.html file
    sudo tee /var/www/html/index.html >/dev/null <<EOF
<!DOCTYPE html>
<html>
<head>
    <title>CHIBUIKE NWOSU PROJECT</title>
</head>
<body>
    <h1>Welcome to CHIBUIKE NWOSU PROJECT - AUTOMATING LOAD BALANCER WITH SCRIPTING</h1>
    <p>Public IP: ${PUBLIC_IP}</p>
</body>
</html>
EOF

    # Restart Apache service
    sudo systemctl restart apache2

    echo "Apache configuration completed."
else
    echo "Apache installation or configuration failed."
fi
```