# BASIC LINUX COMMANDS
This is a manual of the most important admin command line utilities and editors for Linux. Created by Georgy St. Georgiev, 2017


# General
Get info about options and usage of a command
  
    man <command> 
    <command> -h OR --help 

Commands lists
    
    cat /bin OR cat /sbin

Info
  
    which <command> # find where a command is stored

Pipes. On Linux often output of a command can be piped further as an input to another command using the `|` pipe sign. 
  
    <cmd 1> | <cmd 2>

# System
Find out info about your system.

Kernel

    cat /etc/lsb-release
    uname -a
    uname -m

Resources usage (CPU, memory)
  
    top
    free -m

List devices (CPU, USB, GPU)
  
  lscpu
    lsusb
    lspci | grep -i nvidia
    lspci -v | grep -e ^0 -e driver
    
Filesystem
  
    df -h # partitions
    lsblk # partition tree

Reboot/shutdown
  
    reboot
    shutdown now

## Processes
Everything on Linux run as part of a process. 

Find process by name

    ps aux | grep <name> # find id by name

Kill process by id

    kill <PID> # stop pid
    kill -KILL <PID> # force stop pid
    kill -HUP <PID> # reload
    killall <name> # kill all process with some name
    pkill -9 <name> # similar to the above

## Users

Add user
  
    useradd <username>

Password

    passwd # create or add password

Edit sudo users
  
    visudo

Modify user
    
    usermod -d /some/directory
    usermod -a -G groupName userName # add user to group

Switch users
    
    su <username>

User info
    
    whoami # current user
    who # all logged in users
    id # current user groups
    cat /etc/group # list groups
    pwd # current dir
  
User config files
    
    ~/.bashrc
    ~/.profile

### Storage
Info: [ubuntu's page](https://help.ubuntu.com/community/InstallingANewHardDrive)

List partions 
  fdisk -l # list partionsubuntu
  lsblk
  df -T # partitions formatting

Mounting

    mount -t auto -v <partition> <mount_point> # simple mount
    
    mount -o umask=0026,gid=1000,uid=1000 <partition> <mount_point> # mount with permissions
    
    mount -t "ntfs" -o "uhelper=udisks2,nodev,nosuid,uid=1000,gid=1000 dmask=0077,fmask=0177" "/dev/mmcblk1p1" "/media/ubuntu/ml-hdd"
    
    umount <partition> # unmount
    
    mount -t "ntfs" -o "uhelper=udisks2,nodev,nosuid,uid=1000,gid=1000 dmask=0077,fmask=0177" <partition> <mount_point> # mount with NTFS and some permissions    

Partition 

    fdisk <device_name> # partition
    mkfs.<filesystem_type> <device_name> # format
    sudo mkfs -t <filestyme_type> <device_name> # make filesystem on a device

Automount options
  
    vi /etc/fstab
  
## NETWORK
List connections
    
    ifconfig

Connect to WiFi
    
    nmcli d wifi connect <WiFiSSID> password <WiFiPassword> iface wlan0

Monitor 
    
    netstat 
    netstat -ntlp | grep LISTEN # listening ports

Local redirects
  
    /etc/hosts

## Files and dirs
When using <filepath>, we mean relative or absolute path to file + <filename>. Similarly for directories. 

Find 

    find <search in this folderpath> -name <search name> -type <f for file or d for dir> 

Create

    touch <filepath> # create a file
    mkdir <dirpath> # create a folder/directory

Copy
    
    cp <filepath> <new filepath> # copy file
    cp -R <dirpath> <new dirpath> # copy dir
    scp # used to copy between servers
    rsync # used to sync folders between servers

Move or Rename
  
    mv <dir path> <new dir path> # moves to a new dir if it exists or renames the current according to the new path
    
    mv <filepath> <new filepath or dir path> # moves to new dir or renames if filepath is instead specified.

Delete/Remove

    rm <filepath> # delete a file
    rm -rf <dirpath> # delete a folder/directory

File
    
    file <filepath> # type
    du -h # list file sizes in the current folder
    du -h <filepath> # file size
    sha1sum <filepat> # SHA-1 checksum
    md5sum <filepath> # MD5 checksum

Archive 
    
    tar -c <filename> # arthcive
    tar -xf <filepath> # unarchive

File applications 
- Create: `touch`
- Create, Edit, Read: `vi`, `nano` 
- Read: `less`, `tail`, `head`, 
- Read, Write: `cat`, `echo`

Cat 
    
    cat mytext.txt mytext2.txt > newfile.txt # concatenates 2 files in one
    cat mytext.txt >> another-text-file.txt # append content of one file to another

Echo  
    
    echo "My Shopping List" > list.txt # write to file
    echo "My Shopping List" >> list.txt # append to file 

### SSH

    ssh -p <port> <username>@<hostname>:<dirpath>
    ssh -i ... like above # use with certificates
    ssh-keygen # generate a key. Keys are usually in ~/.ssh


