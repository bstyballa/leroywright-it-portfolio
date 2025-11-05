# Case Study: User Can Ping IP Addresses but Cannot Resolve Domain Names

## Scenario
A user reports that they can access internal and external hosts using IP addresses (e.g., `ping 8.8.8.8` works), but they cannot access websites or services using domain names (e.g., `ping google.com` fails).

This indicates that:
- **Network connectivity is working**
- **DNS resolution is failing**

---

## Environment
- Client Device: Windows 10 workstation
- Network Type: Office LAN (DHCP assigned addressing)
- Default Gateway: 192.168.1.1
- DNS Server (expected): 8.8.8.8 (Google DNS)

---

## Symptoms
| Test | Result | Interpretation |
|------|--------|----------------|
| `ping 8.8.8.8` | Successful | The device has full IP connectivity to external networks |
| `ping google.com` | Fails | Device cannot resolve domain names |
| Browser access to websites | Fails | Applications rely on DNS, so they fail as well |

---

## Initial Analysis Using OSI Model
| OSI Layer | What Was Tested | Result | Meaning |
|----------|----------------|--------|---------|
| Layer 1–3 | IP routing/connectivity | Working | Problem is not physical or routing-related |
| Layer 4 | Transport communication | Working | Ports are not blocked |
| **Layer 7** | **DNS name resolution** | **Failing** | Problem isolated to DNS configuration |

---

## Troubleshooting Steps

**Finding:**
- DNS server was set to **192.168.50.50**, which is not a valid DNS server on this network.

### 2. Test DNS server response

**Result:** Request timed out  
→ Confirms DNS server is not responding.

### 3. Manually set a known working DNS server


### 4. Flush DNS Cache and Retry


**Result:** Domain name now resolves correctly ✅

---

## Root Cause
The system was configured to use an **incorrect DNS server**, preventing hostname-to-IP resolution.

---

## Resolution
Updated DNS server to a valid and reachable resolver:
- Primary DNS: **8.8.8.8**
- Secondary DNS: **1.1.1.1**

Cleared DNS cache and verified browsing functionality.

---

## Outcome
| Before Fix | After Fix |
|------------|-----------|
| Could only ping using IPs | Can access websites normally |
| Domain lookups failed | DNS resolution restored |

---

## Key Takeaways (Interview Points)
- If a host can reach IPs but not URLs → **Check DNS first**
- DNS issues commonly appear as “internet down” reports
- Use **`nslookup`** to test DNS resolution directly
- Always verify DHCP is providing correct DNS settings

---

## Demonstrated Skills
- Practical network troubleshooting
- DNS fundamentals
- OSI Model reasoning
- Windows network configuration commands
- Clear issue documentation

### 1. Check Current IP Configuration

