# Denial of Service

## Concepts

- Reduce availability
- Restrict access
- Prevent access
- Flood target

## Impact

- Loss of goodwill
- Disable networks
- Disable organization
- Finacial loss

## Detection

- Actively profile the network
- Change point anylasis

## Distributed DOS

- Attacker creates multiple zombies to flood a target. (aka "botnet")

## Techniques

- Bandwidth flood
- SYN flood (Manipulation of the TCP 3 way handshake)
- ICMP flood (8 Req, 0 Reply)
- UPD flood
- Peer-to-peer
- Application flood (Jam)
- Permanent
  - Phlashing
  - Bricking
  - Sabatoge

## Countermeasures

- Absorb it
- Degrade
- Shut down non critical services
- Neutralize botnet
- Deflect
- Forensics
- Keep software update to date / patches
- Awareness
- Traffic Analysis
- Detect spoofed addresses
- Ingress / Egress Filtering
- TCP intercept
- Load Balancing / Throttling
- Hardening
- Encryption
- Dedicated hardware (Cisco, Forti DDoS, Arbor)