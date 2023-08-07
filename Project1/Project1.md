# Linux Commands with File Manipulation, Permissions and Ownership.

Linux is a family of open-source Unix-like operating systems based on the Linux kernel, an operating system kernel first released on September 17, 1991, by Linus Torvalds. Linux is typically packaged as a Linux distribution, which includes the kernel and supporting system software and libraries, many of which are provided by the GNU Project.

This project PBL(Project Based Project) that gives you the hands on experiences on how the Linux cammds can be used for File Manipulation, File Permissions and File Ownership, these are real life projects as can be seen in our day to day Linux commands applications, In other to excute these Linux cmds we must have the Linux OS installed on your PC as these are cmds runs on the CLI(a console that interacts with the system).

After installaton of the Linux machine on the system, you will update to the latest using the below sudo cmds:

>su root

>sudo su

>adduser vboxuser sudo

>su vboxuser

>sudo apt update

>sudo apt upgrade

![Image](<File Manipulation-sudo cmds.png>)

![Alt text](<File Manipulation-sudo cmds2-1.png>)


## File Manipulation with Basic Linux Commands

* **pwd** - command is used to know your Present working directory
* **cd** - to create and navigate through the different file and directories.
* **ls** - list the files and directory within the system **ls -r** list the subdirectories, **la -a** shows hidden/visible files
* **cat** command - creates a file or file extension depending on what you intended to create
* **tac** command - it deplays the content of the file in a reverse other.

![Image](LinuxCommands(Ls,pwd,cd).png)

* **cp** - copies files/directories to another content
* **mv** - can be used to either move or remain file/directories 
* **mkdir** - its used to creat a directory
* **rmdir** - used to remove directory, adding the **-p** can be used to remove or delete directory containing a file
* **rm** - remove file/files from a directory
* **touch** - Creates a file

![Image](<File Manipulation-cmds rm5.png>)

* **head** command - prints the first lines of one or more files (or piped data) to standard output. By default, it shows the first 10 lines
* **tail** command - shows you data from the end of a fil
* **diff** command - Is used to compare directories in Linux To use the diff command, you will have to follow a simple syntax: **diff -qr deploy1.yml deploy2.yml**

## File Permission and Ownership













