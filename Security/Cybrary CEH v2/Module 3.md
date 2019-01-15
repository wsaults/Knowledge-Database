# Module 3 Scan Enumeration

## 3.1 TCP Header flags Three-way handshake

- SYN
- SYN/ACK
- ACK

## More TCP Header flags

- RES
- FIN
- PSH
- URG

## 3.2 Banner Grabbing

> Allows us to see what operating system is in use

### Fragmentation

- breaking down packets to bypass intrusion detection.
 > Note: Use Colasoft packet builder

## ICMP

 > Internet control message protocol

[icmp](/images/icmp.png)

### ICMP Continued

ICMP Message type 3:

- 0 = Destination network unreachable
- 1 = Destination host unreachable
- 6 = Network unknown
- 7 = host unknown
- 9 = Network administratively prohibited
- 10 = Host administratively prohibited
- 13 = Communication administratively prohibited

## Port scanning

- Full-open (TCP Connect and 3 way handshake. easy to detect)
- Half-Open (Stealth or SYN, no completion of 3 way handshake)
- Inverse TCP: uses FIN, URG, PSH flags. No response means port is open.
- XMAS: Does not work on windows (RFC 793)
- ACK: ACK packet sent and header reviewed for RST packet TTL 64<
- IDLE: spoofed IP address

## 3.3 Live systems lab

- nmap
- ping3