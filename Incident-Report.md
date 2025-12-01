# Incident Report – Large-Scale Data Exfiltration via SharePoint & TLS (Real Incident)

## 1. Summary

A customer reported extreme internet slowness affecting the entire site. Firewall telemetry revealed that one internal workstation was performing sustained, high-volume outbound uploads that completely saturated the network's upstream bandwidth. Over the course of ~2.75 hours, the endpoint uploaded more than **100 GB** of data to SharePoint cloud storage.
After SharePoint access was blocked, the same workstation attempted to exfiltrate data via **SharePoint Web**, and later via **generic TLS/SSL**, indicating likely compromise or intentional data theft. Temporary containment was implemented at the firewall level, and the customer was strongly advised to escalate to their cybersecurity team.

## 2. Impact

- Entire site’s upstream bandwidth maxed out  
- Users unable to work online  
- Continuous exfiltration attempts across multiple days  
- Threat actor demonstrated adaptation to blocking controls  
- Endpoint likely compromised and unsafe for continued use  

## 3. Affected Systems

- **Source Host:** REDACTED  
- **Role:** End-user workstation  
- **User:** Unknown/Not provided  
- **OS:** Windows  

## 4. Detection Details

The exfiltration was identified using firewall monitoring tools displaying:

- Per-host bandwidth consumption  
- Application usage (SharePoint traffic)  
- Destination domains  
- Session size (bytes uploaded)  
- Duration and throughput  
- Traffic patterns (sustained multi-hour upload)  

## 5. Timeline

### **Day 1**
- Customer reports crippling internet slowness  
- Firewall shows one host uploading >100GB  
- Destination: SharePoint (cloud app)  
- **Action:** Blocked SharePoint in firewall  
- **Recommendation:** Escalate to cyber team  

### **Day 2**
- Same host resumes heavy uploading  
- Destination: SharePoint Web (browser-based)  
- **Action:** Blocked SharePoint Web  
- **Recommendation:** Repeat escalation  

### **Day 3 (Monday)**
- Customer again reports severe slowness  
- Host now uploading via generic TLS/SSL  
- **Action:** Blocked TLS/SSL upload attempts  
- Network returns to normal  
- **Critical Recommendation:**  
  - Isolate endpoint  
  - Treat as compromised  
  - Contact cybersecurity team immediately  

## 6. Indicators of Compromise

- Excessive outbound upload traffic  
- Cloud storage destinations: `*.sharepoint.com`  
- Use of SharePoint Web after App-ID blocks  
- Use of encrypted TLS/SSL channel to evade restrictions  
- Upload totals exceeding 100GB  
- Behavior persisted for multiple days  

## 7. MITRE ATT&CK Mapping

- **TA0010 – Exfiltration**  
- **T1567.002 – Exfiltration to Cloud Storage (SharePoint)**  
- **T1048 – Exfiltration Over Alternative Protocol (TLS)**  
- **T1071.001 – Application Layer Protocol: HTTPS**  
- **T1020 – Automated Exfiltration**  
- **T1090 – Use of Alternate Channels**  

## 8. Containment Actions

- Blocked SharePoint application  
- Blocked SharePoint Web  
- Blocked TLS/SSL uploads from the offending host  
- Verified throughput returned to normal  
- Recommended immediate workstation isolation  
- Provided escalation path for full forensic response  

## 9. Recommendations

- Isolate endpoint for forensic analysis  
- Perform malware scan/EDR analysis  
- Investigate cloud access logs in SharePoint/Azure  
- Reset credentials associated with the endpoint  
- Evaluate whether insider threat is possible  
- Implement DLP policies  
- Reinforce firewall ruleset for outbound uploads  
- Monitor for similar upload patterns across site  

## 10. Conclusion

This incident represents a likely compromise of a workstation engaging in deliberate, persistent data exfiltration attempts. Firewall telemetry was essential in detecting the activity and preventing further exfiltration. While temporary containment measures were successful, full remediation requires cybersecurity team involvement and endpoint isolation.
