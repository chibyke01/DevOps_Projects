# ANSIBLE REFACTPRING, ASSIGNMENTS AND IMPORTS
In this project we I will be refactoring ansible code, create assignments, and use the the imports functionality. the import functionality allows us to effectively re-use previously created playbooks in a new playbook, it allows for task organisation and reuse when needed.

**Code refactoring** is the process of restructuring existing code—changing the factoring—without changing its external behavior. Refactoring is intended to improve the design, structure, and/or implementation of the program, while preserving its functionality. Potential advantages of refactoring may include improved code readability and reduced complexity; these can improve the source code's maintainability and create a simpler, cleaner, or more expressive internal architecture or object model to improve extensibility. Another potential goal for refactoring is improved performance.

## Refactoring ansible code by importing other playbooks into site.yml
However to start this project we need to make some changes to our Jenkins job such that every new changes in the code creates a seperate directory which been saved in the jenkins server, although this would consume a lot of space by saving all builds, but however to solve this its advisable to allow for a specific number of builds-this set up will make more sense during the project execution.

## **Jenkins Job Enhancement**
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



