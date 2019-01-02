# Hacking Web Servers

## Prodcucts

- IIS
- Apache
- Nginx
- Google
- Lighttpd

## Impact

- Web defacement
- Compromise
- Data tampering
- Theft
- Pivot points

## Techniques

- Directory Traversal
- HTTP response splitting (forcing the web server to send multiple responses back)
- Web cache poison
- SSH brute force
- MiTM
- Password cracking (Dictionary, brute force, hybrid)
- Form tampering
- Command injection
- Cookie tampering
- Buffer overflow
- DOS
- CSRF (Cross site request forgery)
- SQL Injection
- XSS
- Session Hijack

## Why it happens

- Unnecessary files, backups...
- Sec conflict vs functionality
- Default settings
- Permissions (RWX)
- Misconfigurations
- Default accts (01 = Admin)
- Security flaws / bugs
- Temp SSL
- Improper Auth
- No hardening
- Joomla, Drupal, Wordpress
- Verbose errors
- Anyonymous users
- Sample Configs / Scripts
- Remote Admin
- Unnecessary services
- Mis configurations

## Methodology

1. Info gathering
2. Footprint
3. Mirroring
4. Vuln scan
5. Exploitation (Metasploit)

## Countermeasures

- Patche management process
- Alt sites / alt servers
- Test in non-prod env
- Backups
- Hire me!
- Protocol analysis
- Monitor accts
- Monitor files / dir
- Encryption
- Good architecture
- Vulnscan (nikTo, Nessus)
- DLP (Data loss prevention)