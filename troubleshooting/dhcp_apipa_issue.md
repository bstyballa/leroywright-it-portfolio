# Case Study: Device Shows `169.254.x.x` (APIPA) and Cannot Access Network

## Scenario
A user reports that they cannot access the internet or internal network resources.  
Checking their IP address reveals it is in the **169.254.x.x** range.

This automatically indicates:
- The device **failed to receive an IP address from DHCP**
- Windows assigned an **APIPA** address (Automatic Private IP Addressing)

---

## Environment
- Client Device: Windows 10 workstation
- Network Type: Office LAN
- DHCP Server: 192.168.1.1 (Router-based DHCP)
- Expected Address Range: 192.168.1.0 /24
- Default Gateway: 192.168.1.1

---

## Symptoms
| Test | Result | Interpretation |
|------|--------|----------------|
| `ipconfig` | Shows `169.254.x.x` | DHCP server did not assign an IP |
| `ping 192.168.1.1` | Fails | No local network connectivity |
| `ping 8.8.8.8` | Fails | No internet connectivity |
| Other devices on the same network | Working normally | Problem is isolated to the client, not the network |

---

## Root Cause Theories
1. Ethernet cable unplugged or damaged  
2. Network interface disabled or malfunctioning  
3. Port on switch is down  
4. DHCP server is unreachable  
5. DHCP scope exhausted (no available IPs)  
6. Local firewall or VPN overwriting network configuration  

---

## Troubleshooting Steps (OSI Layer Method)

| Layer | Diagnostic Step | Command / Action | Result | Meaning |
|------|----------------|----------------|--------|---------|
| **Layer 1** | Check cable & NIC link lights | *Visual / Device Manager* | Cable secure & NIC active | Physical layer OK |
| **Layer 2** | Verify interface state | `ipconfig /all` | Adapter enabled | Data Link OK |
| **Layer 3** | Attempt DHCP renewal | `ipconfig /release` → `ipconfig /renew` | Renewal failed | Confirms DHCP issue |
| **Layer 3/4** | Ping DHCP server | `ping 192.168.1.1` | Fails | Device cannot reach gateway |
| **Layer 2/3** | Check switch port status | Admin verified switch port was **disabled** | Root Cause Found ✅ |

---

## Resolution
- Enabled the switch port for the user’s workstation
- Verified link light came on
- Renewed DHCP lease:

- 
Client obtained a valid address:


---

## Outcome
| Before Fix | After Fix |
|------------|-----------|
| Device stuck in `169.254.x.x` (APIPA) | Device received a valid DHCP address |
| No network or internet access | Full LAN and internet connectivity restored |

---

## Final Root Cause
**User’s switch port was disabled**, preventing DHCP lease requests from reaching the server.

---

## Key Takeaways (Interview Talking Points)
- `169.254.x.x` means **"DHCP server not reachable"**
- Always isolate DHCP failures using:

- Use OSI to test from **Physical → Network → Application**
- Switch port issues are a **very common** real-world cause of DHCP failure

---

## Demonstrated Skills
- Layer-based troubleshooting
- DHCP lease negotiation understanding
- Gateway and LAN connectivity testing
- Professional documentation and communication
