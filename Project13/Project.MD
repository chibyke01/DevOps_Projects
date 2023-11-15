# ANSIBLE DYNAMIC ASSIGNMENT (INCLUDE) AND COMMUNITY ROLES
In this project will be using the **include** module, this means that all statements are processed only during execution of the playbook, after the statement are parsed(resolved into its component parts and describe their syntactic roles) any changes to the statements encountered during execution will be used.

## Introducing dynamic assignment into our structure.
In the Github respository , create a new folder called **dynamic-assignments**.

However depending on the method used you may or may not have the roles folder in the Github respository, if you used the **ansible-galaxy** then the **roles** directory was created on the **Jenkins-Ansible** server locally, you can choose to create the roles folder manually and the tree structure should look like the below:
```
├── dynamic-assignments
│   └── env-vars.yml
├── inventory
│   └── dev
    └── stage
    └── uat
    └── prod
└── playbooks
    └── site.yml
└── roles (optional folder)
    └──...(optional subfolders & files)
└── static-assignments
    └── common.yml
```

The below tree structure shows a complete tree folder structure required for this project as seen below:
```
├── dynamic-assignments
│   └── env-vars.yml
├── env-vars
    └── dev.yml
    └── stage.yml
    └── uat.yml
    └── prod.yml
├── inventory
    └── dev
    └── stage
    └── uat
    └── prod
├── playbooks
    └── site.yml
└── static-assignments
    └── common.yml
    └── webservers.yml
```

The below instruction will be saved in **env-vars.yml** file
```
---
- name: collate variables from env specific file, if it exists
  hosts: all
  tasks:
    - name: looping through list of available files
      include_vars: "{{ item }}"
      with_first_found:
        - files:
            - dev.yml
            - stage.yml
            - prod.yml
            - uat.yml
          paths:
            - "{{ playbook_dir }}/../env-vars"
      tags:
        - always
```

**Note** from the above code **include_vars** syntax is used instead of include, this ie because from Ansible version 2.8, the **include** module is deprecated and the variants of **(include_*)** which are **(include_role, include_task, include_vars)** must be used, also the variants of **import** were also introduced such as **import_role**, **import_task** are used.

Special variavles used such as **{{ playbook_dir }}** and **{{ inventory_file }}**. The **{{ playbook_dir }}** helps ansible to determine the location of the running playbook and also navigate to other path on the filesystem. The **{{ inventory_file }}** dynamically resolve to the name of the inventory file being used and append **.yml** so that it picks up the required file within the **env-vars** folder.

Using a loop **with_first_found** implies that looping through the list of files, the first one found is been used.

**site.yml** file needs to be updated so it can make use of the dynamic assignment, the below shows what the site.yml file should look like
```
---
- hosts: all
- name: Include dynamic variables 
  tasks:
  import_playbook: ../static-assignments/common.yml 
  include: ../dynamic-assignments/env-vars.yml
  tags:
    - always

-  hosts: webservers
- name: Webserver assignment
  import_playbook: ../static-assignments/webservers.yml
```
## Update site.yml with dynamic assignments
**Download Mysql Ansible Role**
For this project we will be using **MySQL role developed by geerlinggy**. To install the role cd to the **ansible-config-mgt** directory and run the below command.
```
git init
git pull https://github.com/<your-name>/ansible-config-mgt.git
git remote add origin https://github.com/<your-name>/ansible-config-mgt.git
git branch roles-feature
git switch roles-feature
```

Inside the **roles** directory install **ansible-galaxy install geerlinggy.mysql** and rename the folder by running **mv geerlingguy.mysql/ mysql**

Upload the changes to GitHub by running the below command, and create a Pull request and merge to the main branch in Github.
```
git add .
git commit -m "Commit new role files into GitHub"
git push --set-upstream origin roles-feature
```

From the roles we have two Load Balancer to use **Nginx** or **Apache**, we can choose which to of the load balancer to use by adding a condition.

**NOTE** Declere a variable in **defaults/main.yml** file inside the Nginx and Apache roles. Name each variables **enable_nginx_lb** and **enable_apache_lb** respectively by setting both values to false **enable_nginx_lb: false** and **enable_apache_lb: false**, set **load_balancer_is_required** value to false.

Update both assignment and site.yml files respectively with the below:

**loadbalancers.yml** file update with the below:
```
- hosts: lb
  roles:
    - { role: nginx, when: enable_nginx_lb and load_balancer_is_required }
    - { role: apache, when: enable_apache_lb and load_balancer_is_required }
```

On the **env-vars\uat.yml** file we define which loadbalancer to use in the UAT environment, by setting the value to **true**. To activate and teh loadbalncer and enable **nginx** we use the below settings as same also work for **apache** loadbalancer just to switch the respective environment to **true** and the other **false**.
```
enable_nginx_lb: true
load_balancer_is_required: true
```


**site.yml** update with the below:
```
     - name: Loadbalancers assignment
       hosts: lb
         - import_playbook: ../static-assignments/loadbalancers.yml
        when: load_balancer_is_required 
```

To test the configuration run each of the environment and run Ansible against each environment.