# IPTABLES

### Installation
``` bash
sudo apt-get install iptables-persistent
```

### List IPTable Current Rules
``` bash
sudo iptables -L
```

### Backup Current IPTable

``` bash
iptables-save > backup.txt
```

### Restore IPTable From File
``` bash
iptables-restore < backup.txt 
```

### Save and Reload IPTables

##### >= Ubuntu 16.04
``` bash
sudo netfilter-persistent save
sudo netfilter-persistent reload
```

##### < Ubuntu 16.04
``` bash
sudo /etc/init.d/iptables-persistent save
sudo /etc/init.d/iptables-persistent reload
```

##### >= CentOS 6
``` bash
service iptables save
```

### Allow Loopback Connections
``` bash
sudo iptables -A INPUT -i lo -j ACCEPT
sudo iptables -A OUTPUT -o lo -j ACCEPT
```

### Allow Established and Related Incoming Connections
``` bash
sudo iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT
```

### Allow Established Outgoing Connections
``` bash
sudo iptables -A OUTPUT -m conntrack --ctstate ESTABLISHED -j ACCEPT
```

### Drop Invalid Packets
``` bash
sudo iptables -A INPUT -m conntrack --ctstate INVALID -j DROP
```

### Block an IP Address
##### Only Drop Packages
``` bash
sudo iptables -A INPUT -s <ip> -j DROP
```
##### Let The Sender Know
``` bash
sudo iptables -A INPUT -s <ip> -j REJECT
```

### Open Port
##### For All IPs
###### TCP
``` bash
sudo iptables -D INPUT -p tcp --dport <port> -j ACCEPT
```
###### UDP
``` bash
sudo iptables -D INPUT -p udp --dport <port> -j ACCEPT
```
##### For Specific IP
###### TCP
``` bash
sudo iptables -A INPUT -p tcp -s <ip> --dport <port> -j ACCEPT
```
###### UDP
``` bash
sudo iptables -A INPUT -p udp -s <ip> --dport <port> -j ACCEPT
```