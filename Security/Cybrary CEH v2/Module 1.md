# Module 1

> Dude: 10 mintue mail for temporary email :-D

## 1.2 Laws EH

- HIPAA (Health)
- PCI-DSS (PDC Data Security Standard) (Payment info)
- SOX (Sarbanes-Oxley Act) (Enron / Protects investors)
- DMCA (Digial Millennium Copyright Act)
- FISMA (Federal Information Security Managment Act)
- ISO/IEC 27001: 2013

## 1.4 Password Crack Lab EH

> Cracking a simple md5 hash using John the Ripper

```cmd
john --format=raw-md5 /usr/share/wordlists/rockyou.txt.gz /root/Desktop/passw.txt --show
```