# ANSIBLE REFACTORING, ASSIGNMENTS AND IMPORTS
In this project we I will be refactoring ansible code, create assignments, and use the the imports functionality. the import functionality allows us to effectively re-use previously created playbooks in a new playbook, it allows for task organisation and reuse when needed.

**Code refactoring** is the process of restructuring existing code—changing the factoring—without changing its external behavior. Refactoring is intended to improve the design, structure, and/or implementation of the program, while preserving its functionality. Potential advantages of refactoring may include improved code readability and reduced complexity; these can improve the source code's maintainability and create a simpler, cleaner, or more expressive internal architecture or object model to improve extensibility. Another potential goal for refactoring is improved performance.

## Refactoring ansible code by importing other playbooks into site.yml
However to start this project we need to make some changes to our Jenkins job such that every new changes in the code creates a seperate directory which will be saved in the jenkins server, although this would consume a lot of space by saving all builds, but however to solve this its advisable to allow for a specific number of builds-this set up will make more sense during the project execution.

## **Step:1-Jenkins Job Enhancement**
1. On the Jenkins-Ansible server, create a new directory called ansible-config-artifact as this will store the artifacts after each builds and change the permission as thiw will give jenkins the access to the directory created.
```
sudo mkdir /home/ubuntu/ansible-config-artifact
sudo chmod -R 0777 /home/ubuntu/ansible-config-artifact
```

2. Follow the below steps to install teh copy artifacts plugins in jenkins.
* Go to Jenkins web console 
* Manage Jenkins
* Manage Plugins 
* Avaliable 
* Copy artifacts, install the plugins.

3. Create a Freestyle project and name it save_artifacts, and configure the settings as seen in the below screenshots

4. The main idea save_artifacts project is to save the artifacts in the created directory **/home/ubuntu/ansible-config-artifact** and to achieve this set see the steps in the below screeshots as it specifies the build steps and source project **ansible** and target directory **/home/ubuntu/ansible-config-artifact**.

5. To confirm that the jenkins set up is fine and working as expected we can make some changes on the README.md file on our Github to see if the changes was successfully build and saved on the save_artifacts. see below screenshot.

## Step:2-Refactor Ansible code by importing other playbooks into site.yml
1. In this step 2 we see how code reuse applies by importing other playbooks. Withing the **playbook** folder, create a new file and name it **site.yml**
2. Create a new folder in root of the repository and name it **static-assignments**. The static-assignment folder is where all other children playbook will be stored.
3. Move **common.yml** file into the newly created **static-assignments** folder.
4. Inside site.yml file import common.yml playbook using the code below:
``` 
---
- hosts: all
- import_playbook: ../static-assignments/common.yml
```
The folder structure of all the created folders and file should look like the below tree structure.
```
├── static-assignments
│   └── common.yml
├── inventory
    └── dev
    └── stage
    └── uat
    └── prod
└── playbooks
    └── site.yml
```

However in other to delete the already installed wireshark on my instance from previous project, I will need to create another playbook under **static-assignments** and name it **common-del.yml**. In this playbook we configure the deletion of **wireshark** utility by adding the below code to the **common-del.yml** playbooks.
```
---
- name: update web, nfs and db servers
  hosts: webservers, nfs, db
  remote_user: ec2-user
  become: yes
  become_user: root
  tasks:
  - name: delete wireshark
    yum:
      name: wireshark
      state: removed

- name: update LB server
  hosts: lb
  remote_user: ubuntu
  become: yes
  become_user: root
  tasks:
  - name: delete wireshark
    apt:
      name: wireshark-qt
      state: absent
      autoremove: yes
      purge: yes
      autoclean: yes
```

Update site.yml playbook with the below information:
```
---
- hosts: all
- import_playbook: ../static-assignments/common-del.yml
```

After the above playbook configuration we need to excute the deletion of wireshark by running the code but first we change directory into the created directory.
```
cd /home/ubuntu/ansible-config-mgt/

ansible-playbook -i inventory/dev.yml playbooks/site.yaml
```

## Step:3-Configure uat webservers with a role webserver
In this step we could write a task to configure Webservers in the same playbook, but it would be too messy, instead we will use a dedicated role to make our configuration resuable.

1. This project step we will lunch two(2) new EC2 instances using RHEL image these instances will be used as uat servers, so we name them Web1-UAT and Web2-UAT.
2. Create a directory called **roles**, and there are two wasy to achieve this - either we create it using the Ansible utility called **ansible-galaxy** inside **ansible-config-mgt/roles** directory **OR** we can create the directory or file structure manually.
After creating it your file structure should look like the tree structure below:
```
└── webserver
    ├── README.md
    ├── defaults
    │   └── main.yml
    ├── handlers
    │   └── main.yml
    ├── meta
    │   └── main.yml
    ├── tasks
    │   └── main.yml
    └── templates
```

3. Update the 