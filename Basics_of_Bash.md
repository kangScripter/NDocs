# Bash #
# What is Bash?

Bash stands for **Bourne Again SHell**.
It’s a command-line interpreter or shell used in Linux, macOS, and sometimes in Windows (via WSL or Git Bash).
You use it to communicate with the operating system by typing commands instead of clicking icons.
# Think of it like this:
GUI (Graphical User Interface) → You click to do tasks
Bash (Command-Line Interface) → You type commands to do tasks
# Example:
Instead of clicking **“Open Folder”**, you can type:

### cd /home/tejaswini/Documents ###

⚙️ **What Bash Can Do:**

# Run Linux commands

ls         # list files
cd /etc    # change directory
pwd        # print current directory


# Automate tasks with scripts

#!/bin/bash
echo "Hello, Tejaswini!"
mkdir myfolder

# Manage servers or networks

ping google.com
ssh user@192.168.1.10

# Install and update software

sudo apt update && sudo apt install nginx

# Work with files

cp file1.txt backup/
rm oldfile.txt

# Where Bash Is Used:

Linux servers (e.g., Ubuntu, CentOS)

macOS Terminal

Windows (via Git Bash, WSL – Windows Subsystem for Linux)

Docker, CI/CD pipelines, DevOps scripts

# Example of a simple Bash script:

Create a file called hello.sh:

#!/bin/bash
echo "Hello! This is my first Bash script." **

# Then run it:

bash hello.sh

# Output:

Hello! This is my first Bash script.

# Summary Table
Feature	Description
Full form        :	Bourne Again Shell
Type             :	Command-line shell / scripting language
Main use	       : Run commands, automate tasks
Default shell in :	Most Linux distributions
File extension	 : .sh
Example command	 : ls, cd, echo, sudo, cat

# Example script (backup.sh):

#!/bin/bash
# This is a Bash script
echo "Starting backup..."
cp /home/user/data /home/user/backup/
echo "Backup complete!"

# Run it:
bash backup.sh
