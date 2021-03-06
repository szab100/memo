
##### Testing HTTP over telnet:

```
telnet www.google.com 80
GET / HTTP/1.1

GET /search?q=telnet HTTP/1.1
host: www.google.com
```

---

###### Testing HTTP over OpenSSL:

```
openssl s_client -connect www.google.com:443
GET /search?q=openssl HTTP/1.1
```

---

##### Common commands:

```
ifconfig
ping 8.8.8.8
traceroute 8.8.8.8
nslookup google.com
netstat (on OSX:  sudo lsof -i -P)
netstat -an | grep LISTEN
netstat -r
hostname
```

---

##### Links:

http://whois.arin.net/

http://www.whatismyip.com/

https://dnsleaktest.com/

---

##### Network (JC)

- Find FQDN (DNS): `cat /etc/hosts`

- Network usage by port, avg:	 `iftop -B`

- Network usage by exe: `nethogs`

- Find network interface speed: `dmesg | grep -i "is Up"`

- Network ports open by program (OSX): `sudo lsof -i`

- SSH port forward (server to client): `ssh user@host -L 3306:localhost:3306`

- SSH X-11 forwarding setup for CentOS server: 

	Edit `/etc/ssh/sshd_config` : enable "X11Forwarding"

	```
	yum install xorg-x11-xauth dbus-x11 liberation-*-fonts gnome-icon-theme
	```

- SSH X-11 forwarding setup for Ubuntu server:

	Edit `/etc/ssh/sshd_config` : enable "X11Forwarding"
	
	```
	apt-get install xbase-clients gnome-icon-theme
	```

- Show all firewall ports open/closed:	`sudo iptables -L -v -n --line-numbers`

- Add firewall exception:

	1. Allow SSH: `iptables -A INPUT -s 0/0 -d 0/0 -p TCP -j ACCEPT --dport ssh`
	2. Allow response to requests:`iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT`
	3. Allow loopback: `iptables -v -A INPUT -i lo -j ACCEPT`
	4. Allow pinging: `iptables -A INPUT -p icmp --icmp-type 8 -j ACCEPT`
	5. Allow http: `iptables -A INPUT -p tcp --dport http -j ACCEPT`
	6. Allow https: `iptables -A INPUT -p tcp --dport https -j ACCEPT`
	7. Change default to DROP: `iptables -P INPUT DROP`
	8. Remove REJECT ALL: `iptables -D INPUT -s 0/0 -d 0/0 -j REJECT --reject-with icmp-host-prohibited`
	9. Save settings:
		- CentOS: `service iptables save`
		- Ubuntu: 
		
			```
			sudo apt-get install iptables-persistent
			sudo service iptables-persistent start
			sudo bash -c "iptables-save > /etc/iptables/rules"
			```

---
