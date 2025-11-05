# Case Study: User Can Ping but Cannot Browse the Web

## Scenario
A user reports that they are able to successfully `ping google.com`, but are unable to load websites in their browser.

This indicates:
- **Network connectivity is working**
- **DNS resolution may or may not be functioning**
- **Web traffic (HTTP/HTTPS) may be blocked or misconfigured**

---

## Environment
- Client OS: Windows 10
- Network: Small office LAN
- Gateway: 192.168.1.1
- DNS Server: 8.8.8.8 (Google DNS)
- Network Type: Wired Ethernet

---

## Symptoms
| Test | Result | Interpretation |
|------|--------|----------------|
| `ping 8.8.8.8` | **Successful** | IP connectivity to internet works |
| `ping google.com` | **Successful** | DNS resolution is working |
| Web Browser HTTP/HTTPS | **Fails** | Suggests application or port-specific failure |

---

## Root Cause Theories
1. Firewall blocking ports **80/443**
2. Proxy settings incorrectly configured in browser
3. Security software interfering with traffic
4. Corrupted browser cache/DNS cache mismatch
5. Misconfigured gateway or routing rules

---

## Troubleshooting Steps (OSI Layer Approach)

| OSI Layer | Diagnostic Action | Result | Conclusion |
|---------|------------------|--------|-----------|
| **Layer 1–2 (Physical/Data Link)** | Verified cable & NIC status | OK | No physical link issue |
| **Layer 3 (Network)** | `ping 8.8.8.8` | Successful | Routing to internet works |
| **Layer 4 (Transport)** | `telnet google.com 443` | **Failed** | HTTPS traffic blocked |
| **Layer 7 (Application)** | Checked browser proxy settings | Proxy ENABLED accidentally | Root Cause Found ✅ |

---

## Resolution
- Disabled incorrect proxy setting:  
  `Settings → Network & Internet → Proxy → Turn Proxy Off`

- Cleared browser DNS cache:


- Restarted browser.

---

## Outcome
| Before Fix | After Fix |
|------------|-----------|
| Could ping but not browse websites | Web access restored successfully |

---

## Final Root Cause
**Incorrect proxy configuration was forcing browser traffic through a non-existent proxy server**, blocking all HTTP/HTTPS communication.

---

## Key Interview Takeaways
- Being able to **ping an external IP confirms network connectivity**
- Being able to **ping a domain confirms DNS resolution**
- **Failure at HTTP/HTTPS layer points to ports 80/443, firewall, or proxy settings**
- Using the **OSI model to guide troubleshooting** speeds up root cause identification

---

## What This Demonstrates (Skills)
- Logical troubleshooting
- Understanding of network layers
- Real-world help desk + network diagnostic workflow
- Ability to document issues professionally
