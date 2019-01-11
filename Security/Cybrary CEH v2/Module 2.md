# Module 2: Footprinting

## 2.1 Footprinting

> This is a technique for gathering information on computer systems and the entities they belong to.

Active: interaction
Passive: publicly available "hands off"

## # Footprinting tools

- [alerts](www.visualping.io)
- [website mirroring](www.httrack.com)
- theharvester (Kali)
- Maltego (Map website/server)
- recon-ng (Kali)
- OSRframework

## 2.2 Google Hacking

- **filetype:type** - searches for only files of a specific type
- **intitle:string** - searches for pages that contain the string in the title
- **inurl:string** - displays pages with the string in the URL
- **site:domain** - displays pages for a specific website or domainv

## 2.3 Nikto lab

```cmd
# e for evasion
# 1 for random encoding
nikto -e 1 -h webscantest.com
```

## 2.4 TheHarvester lab

> Domain reserach

```cmd
# d: domain
# l: limit results
# b: data source
# h: shodan
theharvester -d microsoft.com -l 50 -b google -h myresults.html
```

## 2.5 Google hacking

[google hacking db](https://www.exploit-db.com/google-hacking-database)