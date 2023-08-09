# GIT PROJECT

**GIT** is a version control system (VCS) that assist teams to collaborate and track projects.

To get started with this project I installed the Git, as this comes with a terminal called GitBash, but other terminals can be used (e.g powershell and windows CLI etc.) but you will be required to install the git terminal if you are using any of the compartiable **CLI**.


## Initializing a Git Repository and Making Commits

**1.** Open the GitBash terminal and signed in using your name and email using the below git cmds as this helps to keep record of activities log information for activities carried out by any individual. 

        git config --global user.name <name>
        git config --global user.email <emailaddress>


**2.** Create a directory/folder, open the current directory(cd) and run the init cmd as this will create a new local repository in the system. 

        mkdir DevOps_Git
        cd DevOps_Git
        git init

![image](https://github.com/chibyke01/DevOps_Projects/assets/103823637/eea24879-113f-4591-b56e-46f723a096da)



**3.** Created files with contents inside, used the commit cmd to move the file and its contents to the local respository. 

        touch index.txt
        echo "contents in the file" > "filename.txt"
        git add .
        git commit -m "treat and work to prevent gastrointenstina"

![image](https://github.com/chibyke01/DevOps_Projects/assets/103823637/c7ae11b6-2f0f-41e1-b01f-2396dd946ba4)


## Git Branches
**1.** Created a new git branch, switched to the new branch, added files to the newly created branch and commit the file to the new branch.

        git branch
        git branch New_Git_DevOps
        git switch New_Git_DevOps
        touch filename.txt filename1.txt
        git add .
        git commit -m "The Story Line"

![image](https://github.com/chibyke01/DevOps_Projects/assets/103823637/da1eaa09-23a6-4d4d-b4cd-3968afb187df)
----
![image](https://github.com/chibyke01/DevOps_Projects/assets/103823637/6628d9dd-3d9a-4327-bebb-c0c3ce611e50)


**2.** Switch, Merge and Delete a branch.

        git switch main
        git branch -d New_Git_Devops 
        git merge "the branch to merge"
        git status

![image](https://github.com/chibyke01/DevOps_Projects/assets/103823637/e312f59e-8743-4173-b936-61b13a496e3d)
----
![image](https://github.com/chibyke01/DevOps_Projects/assets/103823637/91545846-1b8d-4258-b991-936e9f63d879)


## Remote Repositories/Connecting to Cloud GitHub Repository

**1.** Create a new repository in the cloud

![image](https://github.com/chibyke01/DevOps_Projects/assets/103823637/4fdd815c-997f-4015-94f6-0af1b84ad442)


**2.** Run the below cmd to push the Local repository to the cloud.

        git remote add origin https://github.com/chibyke01/DevOpsGitBash_Remote.git
        git branch -M main
        git push -u origin main

The below output shows a successful push to the cloud repository as the files created previously can be seen in the screenshot below.

![image](https://github.com/chibyke01/DevOps_Projects/assets/103823637/4b1742f7-adbe-43ae-8276-b55b1ee6d835)


To push or update any file or folder this can be done using the GitBash terminal, create a new file using the GitBash terminal and push to the cloud github.

![image](https://github.com/chibyke01/DevOps_Projects/assets/103823637/39a6f3bf-0c5c-4fa9-b4bd-1797b9686b43)
----
![image](https://github.com/chibyke01/DevOps_Projects/assets/103823637/42c6edc5-cbd4-462f-bbcf-f6ce7ceb676b)


The below screenshot concludes the success of this project.

![image](https://github.com/chibyke01/DevOps_Projects/assets/103823637/3a3db8cc-8101-4452-822f-400a2326e061)






## _Thank you_






