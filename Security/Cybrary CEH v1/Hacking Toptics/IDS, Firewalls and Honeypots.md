# Evading IDS, Firewalls & Honeypots

## Concepts

- Placement
- HIDS - HIPS (Host IDS, Host IPS)
- NIDS - NIPS (Network IDS, Network IPS)
- Port scan
- Firewalking (seeing what firewalls are in place)

## Categories

*I*ntegrity
*P*rofile
*A*nomoly
*S*tatistical
*S*ignature
*K*nowledge
*B*ehavior

## Firewall Architectures

- Bastion host
- Screened subnet
- Multi homed (custom built machine with multiple adapter cards)
- DMZ (Boundaries for the network)
- Packet filters
- Circuit Gateway
- Application Gateway (Proxy)
- Statefull

## Attacks (IDS)

- Centrally logged (DOS)
- Obfuscation
- Create false positives
- Session splicing
- Unicode evasion
- Fragment
- Time to live
- Urgent flag (bypass HIDS)
- Polymorphic shellcode
- Encrypt
- Flood

## Attakcs (FW)

- IP ADDR Spoof
- Source route (out dated)
- Fragments
- IP in place of URL
- Anonymouse websites
- Proxy SURs
- ICMP Tunnel
- Ack Tunnel
- HTTP Tunnel
- MiTM

## Honeypots

- Low / High Interaction

## Tools

- Snort (rules)
- Specter (vm honeypot)

## Countermeasures

- Shot down ports
- Defense in depth
- TCP RST
- Detect 0x90/ polymorphic shellcode
- Patches