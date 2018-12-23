# Nmap

To scan an IP address:

```
nmap 192.168.27.0/24
```

To identify the operating system versions and to send scan TCP ports using the SYN packet:

```
nmap -O -sS 192.168.27.0/24 > hosts.txt
```