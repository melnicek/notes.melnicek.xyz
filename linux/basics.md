## filesystem

| folder | description |
| --- | --- |
| / | The top-level directory is the root filesystem and contains all of the files required to boot the operating system before other filesystems are mounted as well as the files required to boot the other filesystems. After boot, all of the other filesystems are mounted at standard mount points as subdirectories of the root. |
| /bin | Contains essential command binaries. |
| /boot | Consists of the static bootloader, kernel executable, and files required to boot the Linux OS. |
| /dev | Contains device files to facilitate access to every hardware device attached to the system. |
| /etc | Local system configuration files. Configuration files for installed applications may be saved here as well. |
| /home | Each user on the system has a subdirectory here for storage. |
| /lib | Shared library files that are required for system boot. |
| /media | External removable media devices such as USB drives are mounted here. |
| /mnt | Temporary mount point for regular filesystems. |
| /opt | Optional files such as third-party tools can be saved here. |
| /root | The home directory for the root user. |
| /sbin | This directory contains executables used for system administration (binary system files). |
| /tmp | The operating system and many programs use this directory to store temporary files. This directory is generally cleared upon system boot and may be deleted at other times without any warning. |
| /usr | Contains executables, libraries, man files, etc. |
| /var | This directory contains variable data files such as log files, email in-boxes, web application related files, cron files, and more. |


## fundamental commands

| command | description |
| --- | --- |
| whoami | Displays current username. |
|id | Returnsusers identity |
| hostname | Sets or prints the name of current host system. |
| uname | Prints operating system name. |
| pwd | Returns working directory name. |
| ifconfig | The ifconfig utility is used to assign or to view an address to a network interface and/or configure network interface parameters. |
| ip | Ip is a utility to show or manipulate routing, network devices, interfaces and tunnels. |
| netstat | Shows network status. |
| ss | Another utility to investigate sockets. |
| ps | Shows process status. |
| who | Displays who is logged in. |
| env | Prints environment or sets and executes command. |
| lsblk | Lists block devices. |
| lsusb | Lists USB devices |
| lsof | Lists opened files. |
| lspci | Lists PCI devices. |

## user management

| command	| description |
| --- | --- |
| sudo | Execute command as a different user. |
| su | The su utility requests appropriate user credentials via PAM and switches to that user ID (the default user is the superuser). A shell is then executed. |
| useradd | Creates a new user or update default new user information. |
| userdel | Deletes a user account and related files. |
| usermod | Modifies a user account. |
| addgroup | Adds a group to the system. |
| delgroup | Removes a group from the system. |
| passwd | Changes user password. |
