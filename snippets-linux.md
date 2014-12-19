##### Disk:

- Find a file (recursive): `find /usr/share/cacti -name '*.sql'`
- Copy with modification time: `rsync -t sourceFile.txt destPath`
- Copy with modification time and owner/group: `rsync -a sourceFile.txt destPath`
- Make a backup of files in folder: `	rsync -arv inwar/ inwar-bak/`
- Convert zip to gzip: `unzip -p file.zip | gzip > file.gz`
- gzip and keep original file: `gzip -c hugeFile.txt > hugeFile.txt.gz`
- gzip a folder: `tar -czvf folder.tar.gz /path/to/dir`
- Extract a gzipped folder: `tar -xzvf folder.tar.gz`
- What process has a folder/file open: `lsof +D <path>`
- Disk space free on drive: `df -h`
- Disk space of a folder: `du -sh`
- Disk space of subfolders: `du --max-depth 1 | sort -n`
- RAM and swap usage: `free -mt`
- Disk bandwidth usage: `iotop`
- Replace text in all files in a folder (recursive): 
	`find ./ -type f -exec sed -i 's/apple/orange/g' {} \;`
	

---

##### Linux Users:

- Create user: `useradd -m -s "/bin/bash" <username>`
- Set password: `passwd <username>`
- Remove user: `userdel -r <username>`
- Create group:	`groupadd <groupname>`
- Create user and add user to group: `useradd -G <groupname> <username>`
- Add user to group: `usermod -a -G ftp tony`
- Add user to sudoers:
	- on Ubuntu:
		`usermod -a -G sudo <username>`
	- on CentOS:
	
		```
		groupadd sudo
		visudo and add: %sudo ALL=(ALL) ALL
		usermod -a -G sudo <username>
		```
---

##### To install Nano:

- `yum install sudo nano`	
- in ~/.bashrc : `export EDITOR=nano`

---

##### Misc Commands:

- Find what packages use a package: `aptitude why <package>`
- Shutdown server: `shutdown -h 0`
- Find OS version: `cat /etc/issue`
- Remotely share bash: `tmux`
- Find in man: `/term`
- Copy stdout to clipboard over ssh: `| xclip -i`
- Look at auto start services: `chkconfig`
- Restart a service: `service <name> restart`
- Kill a process: `kill -9 <pid>` or `pkill -f <proc_name>`
					
---
					
