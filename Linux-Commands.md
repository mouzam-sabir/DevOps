# Linux Commands
---
# Navigation
- Current location
```
pwd
```
- Go to specific directory
```
cd /home/username
```
- Go to home directory
```
cd ~
```
- Show current Folder (files/folders)
```
ls
```
- Show hidden files
```
ls -a
```
---
# User & Groups
- Show users list
```
cat /etc/passwd
````
- Show usernames only
```
cut -d: -f1 /etc/passwd
````
- Create a new user
```
sudo adduser username
````
- Change password of user
```
sudo passwd username
````
- Delete a user
```
sudo userdel username
````
- Delete a user along with home directory
```
sudo userdel -r username
````
- Show current user groups
```
group username
````
- Create a new group
```
sudo groupadd groupname
````
- Show groups
```
cat /etc/groups
````
- Adding user in group
```
sudo usermod -aG groupname username
```
- Change user username
```
sudo usermod -l newname oldname
````
- Lock user account
```
sudo usermod -L username
````
- Unlock user account
```
sudo usermod -U username
````
- Change user home directory
```
sudo usermod -d /path username
````
- Change user login shell
```
sudo usermod -s /bin/shell username
````
---
# Files and Permissions
- Create an empty file
```
touch file.txt
```
- Set permissions
```
chmod 755 file.txt
```
- Giving execute permission to owner
```
chmod u+x file.txt
```
- Removing execute permission from owner
```
chmod u-x file.txt
```
- Show files detail of present directory
```
ls -l
```
- Change file ownership
```
sudo chown username file.txt
```
- Change file owner and group
```
sudo chown user:group file.txt
```
- rename a file
```
sudo mv file.txt newfile.txt
```
- Move a file
```
sudo mv file.txt /path/to/destination/
```
- Move and Rename a file
```
sudo mov file.txt /path/to/destination/newfile.txt
```
- Delete a file
```
sudo rm file.txt
```
- Look for a text in a folder
```
grep -r "text"
```
---
# Backup and file Transfer
- Compressed Backup
```
tar -cvpzf backup.taz.gz /path
```
- Backup restore
```
tar -xvpzf backup.tar.gz -C /path
```
- Look inside the compress backup file
```
tar -tvf backup.tar.gz
```
- Smart copy - only copy changes
```
rsync -avh source/destination
```
- Copy a file
```
cp source destination
```
---
# Automation
- Cron jobs edit/add karna
```
crontab -e
```
- Show cronjobs list
```
crontab -l
```
- Delete all cronjobs
```
crontab -r
```
- How to write cronjob command
```
* * * * * command
```
Important:
(*) Format: (Time, hour, Date, Month, Weekday) 
30 2 15 * * backup.sh 
means (Do backup after every 15 days at 2:30 am)
---
# System Monitoring
- Live Process list 
```
top
```
- Live Process list with colors and also U can kill a process directly
```
top
```
- Sumamry of the Memory + CPU + swap memory
```
vmstat
```
- Check Disk read/write speed
```
iostat
```
- Check RAM/Swap state
```
free
```
- Check Disk Space
```
df -h
```
- Show disk partition structure
```
lsblk
```
- Look for a specific process
```
ps -p PID -o comm=
```
---
# Extras
- Show current user
```
whoami
```
- System/kernal info
```
uname -a
```
- Commands history
```
hisotry
```
- Info/Manual about a command
```
man command
```
- Kill a process
```
kill PID
```
- Kill a process with name
```
killall processname
```
- Look for IP address
```
ipconfig or ip a
```
- Look for a file
```
find / -name "filename"
```
- How much lines in a file
```
wc -l file.txt
```
---
