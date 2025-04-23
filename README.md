# 🕵️ Network Traffic Analysis: DNS & ICMP Incident Investigation  
*A cybersecurity project analyzing tcpdump logs to diagnose a "destination port unreachable" error*

tcpdumb log for reference:


![Alt text](https://i.imgur.com/renNHPK.png)
## 📝 Cybersecurity Incident Report  

### **Part 1: Summary of the Problem**  
**The UDP protocol reveals that:**  
- A DNS query was repeatedly sent to port 53 (DNS service) but failed with ICMP error messages.  

**Network analysis results show:**  
- ICMP replies returned the error: `"udp port 53 unreachable"` from the DNS server (`203.0.113.2`).  
- Timestamps (e.g., `13:24:32.192571`) indicate retries over 4 minutes, suggesting a persistent service outage.  

**The port noted in the error message is used for:**  
- **DNS resolution** (UDP port 53), critical for translating domain names to IP addresses.  

**The most likely issue is:**  
- The DNS server was **unreachable** or **not listening on port 53**, disrupting access to `yummyrecipesforme.com`.  

---

### **Part 2: Analysis & Root Cause**  
**Time incident occurred:**  
- First observed at **1:24 PM** (timestamp `13:24:32.192571`).  

**How the IT team became aware:**  
- Multiple users reported the error `"destination port unreachable"` when accessing the website.  

**Actions taken to investigate:**  
1. Captured traffic via `tcpdump` during a reproduction attempt.  
2. Analyzed logs, identifying:  
   - Outbound UDP DNS queries (`192.51.100.15 > 203.0.113.2.domain`).  
   - ICMP errors indicating port 53 was unreachable.  

**Key findings:**  
- **DNS service disruption**: No response to UDP queries on port 53.  
- **ICMP diagnostics**: Confirmed the DNS server was online but not servicing requests.  

**Likely cause:**  
- **DNS service crash** or **misconfigured firewall** blocking UDP/53.  
- **Potential DDoS attack**: Repeated queries could indicate malicious traffic overwhelming the server.  

---

## 🔧 Recommended Solutions  
1. **Immediate Mitigation**:  
   - Restart the DNS service or failover to a secondary server.  
   - Verify firewall rules allow UDP/53 traffic.  
2. **Long-Term Prevention**:  
   - Implement **rate limiting** to block query floods.  
   - Deploy **DNSSEC** to prevent spoofing attacks.  

---

## 📂 How to Use This Project  
- **For Recruiters**: Demonstrates **log analysis**, **protocol expertise** (DNS/ICMP), and **incident response** skills.  
- **For Learners**: [Template](https://docs.google.com/document/d/1hwjSRYalxGd-qyRIXWz8LBVuSAgEq0AHXOF_BB7DdrI/template/preview) for analyzing `tcpdump` logs in security investigations.  

**Tools Used**: `tcpdump`.  
**Standards**: RFC 1035 (DNS), RFC 792 (ICMP).  

---
