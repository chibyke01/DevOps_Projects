# SHELL SCRIPTING
A shell script is a text file that contains a sequence of commands for a UNIX-based operating system. It is called a shell script because it combines a sequence of commands, that would otherwise have to be typed into the keyboard one at a time, into a single script.
The shell is the operating system's command-line interface (CLI) and interpreter for the set of commands that are used to communicate with the system.

A shell script is usually created for command sequences in which a user has a need to use repeatedly in order to save time. Like other programs, the shell script can contain parameters, comments and subcommands that the shell must follow. Users initiate the sequence of commands in the shell script by simply entering the file name on a command line.

## Examples of shell script applications
Using a shell script is most useful for repetitive tasks that may be time consuming to execute by typing one line at a time. A few examples of applications shell scripts can be used for include:

* Automating the code compiling process.
* Running a program or creating a program environment.
* Manipulating files.
* Linking existing programs together.
* Executing routine backups.
* Monitoring a system.

In this project of shell scripting we are going to see how these scripts are applied and how they can be used to manipulate and automate process, but before we proceed there are some prequisits we need to have in mind.
* **chmod cmds (chmod +x <name_of_file> or chmod 777 <name_of_file>** - allows you to change the permissions on a file using either a symbolic or numeric mode or a reference file.
* **shebang** - Is a combination of the **#** (pound key) and **!** (exclamation mark). It is used to specify the interpreter with which the given script will be run by default.

This script can be generated/run using any code interface or editor, in the course of this project I will be using the below:
* **vscode terminsl**, 
* **bash terminal** and the 
* **vi editor** interface in bash terminal.

## Shell Scripting Syntax Elements
**Using the if-else script to execute task (Using Vscode/VI editor/Bash terminal)**

```
#!/bin/bash

# Example script to check if a number is positive, negative, or zero

read -p "Enter a number: " num

if [ $num -gt 0 ]; then
    echo "The number is positive."
elif [ $num -lt 0 ]; then
    echo "The number is negative."
else
    echo "The number is zero."
fi
```
However to call up the vscode from the bash terminal I used **code .** but before that we need to create a file with a **.sh**.

`touch chibuike_script.sh`

`./chibuike_script.sh`

`code .`

running the above will open a vscode terminal and you can either paste or type your acript on the vscode page and save, after which run the below code on the vscode terminal

`./chibuike_script.sh`

**Using Vscode**
![Alt text](image.png)

**Using the Vi editor**
![Alt text](image-3.png)

**Using the bash terminal**
![Alt text](image-1.png)

Let us run another script this time we need to create a directory and a file in the directory to save the script.
```
mkdir shell-scripting
cd shell-scripting
touch user-input.sh
```

with the vi editor open the file user-input.sh, you can either type or paste the script and use :wq! to save and exit.

`vi user-input.sh`
```
#!/bin/bash

# Prompt the user for their name
echo "Enter your name:"
read name

# Display a greeting with the entered name
echo "Hello, $name! Nice to meet you."
```
`:wq!`

On the terminal we need to allow permission for the file but in some cases you can run the cmd if you have the required permissions

`chmod +x user-input.sh`

`./user-input.sh`

![Alt text](image-4.png)

## Directory Manipulation and Navigation
In this project the script will create a directory cd the directory and create two file in it, list the files created, move back one level up, remove the directory that was created and its contents and will list the files in the directory, but before we proceed we need to create a .sh file in the bash terminal, open the fil eusing the vi editor and paste the script before running it.

`touch navigating-linux-filesystem.sh`

`vi navigating-linux-filesystem.sh`
```
#!/bin/bash

# Display current directory
echo "Current directory: $PWD"

# Create a new directory
echo "Creating a new directory..."
mkdir my_directory
echo "New directory created."

# Change to the new directory
echo "Changing to the new directory..."
cd my_directory
echo "Current directory: $PWD"

# Create some files
echo "Creating files..."
touch file1.txt
touch file2.txt
echo "Files created."

# List the files in the current directory
echo "Files in the current directory:"
ls

# Move one level up
echo "Moving one level up..."
cd ..
echo "Current directory: $PWD"

# Remove the new directory and its contents
echo "Removing the new directory..."
rm -rf my_directory
echo "Directory removed."

# List the files in the current directory again
echo "Files in the current directory:"
ls
```
`chmod +x navigating-linux-filesystem.sh`

`./navigating-linux-filesystem.sh`

![Alt text](image-5.png)

## File Operations and Sorting
In this project the script creates three file(file1.txt, file2.txt and file3.txt) displays the files in their current order, sorts them alphabetically, saves the sorted files in sorted_files.txt, displays the sorted_files_sorted_alphabetically.txt and displays the content of the final sorted file.

`touch sorting.sh`

`vi sorting.sh`
```
#!/bin/bash

# Create three files
echo "Creating files..."
echo "This is file3." > file3.txt
echo "This is file1." > file1.txt
echo "This is file2." > file2.txt
echo "Files created."

# Display the files in their current order
echo "Files in their current order:"
ls

# Sort the files alphabetically
echo "Sorting files alphabetically..."
ls | sort > sorted_files.txt
echo "Files sorted."

# Display the sorted files
echo "Sorted files:"
cat sorted_files.txt

# Remove the original files
echo "Removing original files..."
rm file1.txt file2.txt file3.txt
echo "Original files removed."

# Rename the sorted file to a more descriptive name
echo "Renaming sorted file..."
mv sorted_files.txt sorted_files_sorted_alphabetically.txt
echo "File renamed."

# Display the final sorted file
echo "Final sorted file:"
cat sorted_files_sorted_alphabetically.txt
```
`chmod +x sorting.sh`

`./sorting.sh`

![Alt text](image-6.png)

## Working with Numbers and Calculations
THis script defines two variables num1 and num2 with numeric values, performs basic arithmetic operations and displays the results, it also raised the num1 to a power of 2 and calculate the square root of num2 and displays the results.

`touch calculations.sh`

`vi calculations.sh`
```
#!/bin/bash

# Define two variables with numeric values
num1=10
num2=5

# Perform basic arithmetic operations
sum=$((num1 + num2))
difference=$((num1 - num2))
product=$((num1 * num2))
quotient=$((num1 / num2))
remainder=$((num1 % num2))

# Display the results
echo "Number 1: $num1"
echo "Number 2: $num2"
echo "Sum: $sum"
echo "Difference: $difference"
echo "Product: $product"
echo "Quotient: $quotient"
echo "Remainder: $remainder"

# Perform some more complex calculations
power_of_2=$((num1 ** 2))
square_root=$(awk "BEGIN{ sqrt=$num2; print sqrt }")

# Display the results
echo "Number 1 raised to the power of 2: $power_of_2"
echo "Square root of number 2: $square_root"
```
`chmod +x calculations.sh`

`./calculations.sh`

![Alt text](image-7.png)

## File Backup and Timestamping
This script defines the source directory and back up directory paths, it then creates a timestamp using the current date and time, and create a backup directory with the timestanp and append it to its name, the script then copies all the files from the source directory to the backup directory using the cp command with -r option for recursive copying. after the operation it displays a message indicating the completion of the backup process and shows the path pf the backup directory with time stamp. This script will also run on the vscode.

`touch backup.sh`

`vi backup.sh`
```
#!/bin/bash

# Define the source directory and backup directory
source_dir="/path/to/source_directory"
backup_dir="/path/to/backup_directory"

# Create a timestamp with the current date and time
timestamp=$(date +"%Y%m%d%H%M%S")

# Create a backup directory with the timestamp
backup_dir_with_timestamp="$backup_dir/backup_$timestamp"

# Create the backup directory
mkdir -p "$backup_dir_with_timestamp"

# Copy all files from the source directory to the backup directory
cp -r "$source_dir"/* "$backup_dir_with_timestamp"

# Display a message indicating the backup process is complete
echo "Backup completed. Files copied to: $backup_dir_with_timestamp"
```
`chmod +x backup.sh`

`./backup.sh`

![Alt text](image-8.png)
![Alt text](image-10.png)

**N/B** You can also confirm the number on the  backup folder is same with the backup number on the bash terminal **backup_20230817181905
** 

* Using the Vscode to run the script

`touch backup.sh`
`code .`

On the vscode terminal run the below cmd.

`./backup.sh`

![Alt text](image-9.png)

**_Thank You_**




