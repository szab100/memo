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
- Run the last command with sudo: `sudo !!`

---

##### top:

`top` - to display info about processes  
`?`  - to get help when `top` is running  

- Linux (CentOS):

`<` - move sort field left  
`>` - move sort field right  
`O` - to select the sort field  
`n` - to sort by _memory_ usage  
`k` - to sort by _CPU_ usage  

- OS X:

```
top -o cpu
top -o mem
```

---

##### :key: SSH

- To set up SSH public-key authentication to connect to a remote server:

```
scp ~/.ssh/id_rsa.pub username@server:
ssh username@server
cat id_rsa.pub >> ~/.ssh/authorized_keys
cat ~/.ssh/authorized_keys
rm id_rsa.pub
exit
ssh username@server
```

---

##### :key: ROT13 cipher 

- with `tr` translate characters command:

```bash
# Map upper case A-Z to N-ZA-M and lower case a-z to n-za-m
echo "The Quick Brown Fox Jumps Over The Lazy Dog" | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```