# Toolbelt

## Analize network traffic

- Snort
- Wireshark

Example wireshark filter

```txt
smb and tcp and ip.addr == 198.51.100.50
```

- hexdump

## Network mapping

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

## DOS (Denial of service)

- hping3

## Password cracking

- Cain & Able
- pwdump7
- [LMHash](http://www.tobtu.com/lmntlm.php)

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