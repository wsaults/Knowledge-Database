# Session Hijacking

> Note: Try to predict the session tokens

## Why

- No account lockout
- Insecure session handling
- Small session Id's
- Weak generation algorithms
- Infinate session time
- Cleartext
- Predictable
- Sequence #'s

## Concepts

- 3 way hanshake
- Spoofing vs. hijacking
- Active vs passive
- Network vs application
- Session ID
- Man in the browser "BURP"
- MiTM
- XSS (Cross site scripting)

## Diagram

Victim -----> Service
    /\       |  /\
     \       |  |
      \      V  |
        Attacker

## How

1. Sniff traffic / monitor
2. Desync victim
3. Take over session
4. Whatever you want

## Where

- URL Argument
- Hidden form field
- Cookies

## Techniques

- Calculate session Id's
- Steal session
- Brute forcing
- Forged ICMP / ARP

## Network Level

- Blind hijacking (No immediate response)
- UDP Hijack
- TCP / IP
- RST Hijack (Sending a reset packet to track the client or server)
- IPSpoof

## Countermeasures

- Encryption (HTTPS, SSH)
- Good RNG's
- Generate session after login
- Logout functionality
- 2 Factor challenge
- Education
- Switches vs hubs / Shared medium (AP)
- Strong Auth
- ARPWatch
- Defense in depth (Use a variety of counter measures)
- Timeout()
- Keep up to date
- IPSEC