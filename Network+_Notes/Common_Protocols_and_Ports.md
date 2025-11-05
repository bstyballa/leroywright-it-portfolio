# Common Ports, Protocols, and OSI Layers (Network+ Study Reference)

| Port | Protocol / Service | Use Case / Purpose | Transport | OSI Layer (Functionally) |
|------|-------------------|-------------------|-----------|--------------------------|
| 20/21 | FTP | File transfer (clear text) | TCP | Layer 7 – Application |
| 22 | SSH | Secure remote terminal access | TCP | Layer 7 – Application |
| 23 | Telnet | Remote access (insecure) | TCP | Layer 7 – Application |
| 25 | SMTP | Sending email | TCP | Layer 7 – Application |
| 53 | DNS | Translates domain names ↔ IP | TCP/UDP | Layer 7 (Application) interacts with L3 addressing |
| 67/68 | DHCP | Automatic IP assignment | UDP | Layer 7 – Application |
| 69 | TFTP | Simple file transfers (no auth) | UDP | Layer 7 – Application |
| 80 | HTTP | Web browsing (unencrypted) | TCP | Layer 7 – Application |
| 110 | POP3 | Email download to client | TCP | Layer 7 – Application |
| 143 | IMAP | Email sync and server mailbox access | TCP | Layer 7 – Application |
| 443 | HTTPS | Secure web browsing (TLS) | TCP | Layer 7 – Application |
| 445 | SMB | Windows file + printer sharing | TCP | Layer 7 – Application |
| 389 | LDAP | Directory services / Active Directory lookups | TCP/UDP | Layer 7 – Application |
| 636 | LDAPS | Secure LDAP | TCP | Layer 7 – Application |
| 161/162 | SNMP | Network monitoring + device management | UDP | Layer 7 – Application |
| 3389 | RDP | Remote desktop (GUI remote control) | TCP/UDP | Layer 7 – Application |

### Quick Memory Tip
Group by function instead of numbers:
- **Web:** 80 / 443  
- **Remote:** 22 / 23 / 3389  
- **Email:** 25 / 110 / 143  
- **File:** 20-21 / 69 / 445  
- **Network Infrastructure:** 53 / 67-68 / 389-636 / 161-162

---

## Why This Matters (Interview Talking Point)
Ports are critical for:
- Troubleshooting blocked services
- Diagnosing firewall issues
- Identifying application failures
- Packet/traffic analysis

Knowing *why* ports matter is more important than just memorizing numbers.

