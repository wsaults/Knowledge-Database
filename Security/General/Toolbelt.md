# Toolbelt

## Recon

- [anywho.com](https://www.anywho.com)
- [spokeo.com](https://www.spokeo.com)
- [yasni.com](https://www.yasni.com)
- nslookup

```cmd
nslookup www.google.com
set type=MX (mail exchange?)
set type=SOA (start of authority)
set type=NS (name server)
set type=a
```

> Note: You can just type nslookup and hit enter to start interactive mode

- Path Analyzer Pro
- ping
- dnsenum (kali)

```cmd
dnsenum virnet.com
```

-hping3

```cmd
hping3 -SU 75.98.175.71
```

-etherape
-nikto

```
nikto -h http://
```

### Analyze network traffic

- Snort
- Wireshark

Example wireshark filter

```txt
smb and tcp and ip.addr == 198.51.100.50
```

- hexdump
- ICMPsrv (tunnel command line application)
- urlSnarf (Kali: sniff HTTP requests) (use wwwstat to analyze pcap output from urlsnarf)
- WebSpy (Kali: displays sniffed urls in the browser in real time)

### Network mapping

- nmap

> The -sT calls the services (protocols) being used on the open ports.

```cmd
nmap -sT 192.168.0.0/24
```

> The -sV calls the versions (programs/services) that are using those open ports.

```cmd
nmap -sT -sV 192.168.0.0/24
```

> You can also use -A to determine each host's Operating System.

### Wireless

- airmon-ng
- airodump
- kismet (packet sniffer)

## Enumeration

- GetAcct / enum4linux
- nbtstat / enum4linux
- netuse
- netstat (TCP / UDP info)
- netdiscover

```cmd
netdiscover -i eth0
```

- macof (packet flooding)

```cmd
macof -i eth0 -n 10
```

- smdclient
- SuperScan (Windows)
- PsTools (Windows)

### Null Session

#### Linux

```cmd
smbclient -I IPADDRESS -L DOMAIN -N -U
```

#### Windows

```cmd
net use \\192.168.92.131\IPC$ /u:"" ""
```

### DOS (Denial of service)

- hping3

```cmd
hping3 -S IP -a IP -p 21 --flood
hping3 -S IP -a IP -p 22 --flood
hping3 -S IP -a IP -p 80 --flood
```

LOIC (Low orbing ion cannon)

### Password cracking

- Cain & Able
- pwdump7
- [LMHash](http://www.tobtu.com/lmntlm.php)
- default passwords lists [phenoelit.org](http://www.phenoelit.org/dpl/dpl.html)
- Link Control Protocol (LCP - Windows)

## Hacking

> Note: sing "Alternative data streams" to hide files

- ADS Spy (detects Alternative Data Streams)
- x.exe (Windows - Adds an X user to the admin users)

- BinText Windows program (view strings at memory locations in a file)

- Internet worm maker thing (script kiddie)
- DELmE's Batch Virus Maker (script kiddie) [cybrary lab](https://www.cybrary.it/video/viruses-worms-delme-lab/)
- JPS Virus maker (script kiddie)
- DriftNet (Kali: capture network traffic including audio)
- macof (Kali: packet flooding)
- SMAC (Windows: change mac address)

### Session Hijacking

- Ferret (Windows)
- Hamster (Windows: Browser tool)
- Burpsuite (Kali: web app hacking, MiTM, session hijacking)

### Web Application Hacking

- Httprecon (Windows)
- ID Serve (Windows)
- wget (Kali)
- DirBuster (Kali)
- wpscan (Kali: Scan WordPress sites)
- BlindElephant.py (Kali: Web app scanner)

```cmd
wpscan --url www.example.com
```

### SQL Injection

> Note: Google search for SQL injection vulnerable sites

```cmd
php?id=
```

- sqlmap (Kali)

## Incident response (Windows)

- Event viewer (Run: `eventvwr`)
- Command prompt (Run: `cmd`)
- Task scheduler `schtasks` (Attacker can use to obtain persistance)
- MSConfig `msconfig` (Attacker can use to obtain persistance)
- Registry edit ("Run": `regedit`)
- Address resolution protocol `arp -a`
- Active network connections `netstat -ano`
- Check hosts file entries for redirects `type %SystemRoot%\System32\Drivers\etc\hosts`
- List currently running services `tasklist /svc`
- File signature verification `sigverif`
- Search for newly created files in the system32 directory `dir /a/o-d/p %SystemRoot%\System32\`
- Static Analysis: "Strings" program
- Dynamic Analysis: "Wireshark" program
- Watch for Registry modifications "RegShot"
- [VirusTotal.com](http://www.VirusTotal.com) for scanning files

## Viewing strings in an executable

- Strings