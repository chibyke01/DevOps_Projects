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

In Linux, they are three(3) types of file permissions: read (r), write (w) and execute (x) permissions. These permissions determine which users can read, write or execute the files.

Files and directories can belong to either the following:

* u   –  Owner of the file
* g   –  Group
* o   –  Others

File permissions are listed using the **ls -l** command. The -l flag lists the file permissions. The permissions are arranged in three sets: the user, group and others respectively.

* **chmod** command(change mode) is used to manage file and directory permissions and determines who can access them.

* **chown** command changes user ownership of a file, directory, or link in Linux. 

![Image](<File Manipulation-cmds chmod7.png>)

![Image](<File Manipulation-cmds chmod8.png>)



* **kill** command can be used when a process becomes unresponsive or is consuming too many resources, you may need to kill it. A root user can kill all processes. You can either add sudo before a command to run it as root, or obtain a root shell with su. Then execute the command.
Killing a process sends a termination message to the given process. There are multiple types of termination messages including:

	* **SIGKILL** – is the ultimate way of killing a process. It will always kill a process and will 	kill the process abruptly, generating a fatal error. SIGKILL should always work. If it does not work, the operating system has failed.

	* **SIGTERM** – SIGTERM attempts to kill a process, but unlike SIGKILL it may be blocked or otherwise 	handled. It can be considered a gentler way of attempting to terminate a process.

* **ps -aux** command is used to get a detailed process list of all processes.    **-a** View processes of all users rather than just the current user. **-u** Provide detailed information about each of the processes, **-x** Include processes that are controlled not by users but by daemons.











