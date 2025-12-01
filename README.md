# Data Exfiltration Detection Using Firewall Telemetry (Real-World Incident)

## Overview

This repository documents the detection and mitigation of a **large-scale data exfiltration attempt** discovered through firewall telemetry at a customer site. The incident involved a single compromised Windows endpoint that uploaded **100+ GB of data within ~2.75 hours** to multiple destinations (SharePoint, SharePoint Web, and finally raw TLS/SSL endpoints) across multiple days.

The upload behavior repeatedly **maxed out the entire site's upstream bandwidth**, causing a near-complete network outage for all users. Initial containment actions were taken at the firewall level, followed by escalation recommendations to the customer’s cybersecurity team.

This case demonstrates the workflow of a real-world detection, investigation, containment, and escalation scenario using firewall logs and traffic analytics.

---

## Environment

- **Customer Type:** SMB/Enterprise hybrid  
- **Firewall Platform:** Next-generation firewall with application control & traffic analytics  
- **Monitored Telemetry:**  
  - Application Identification (App-ID)  
  - User-Agent & TLS fingerprint  
  - Destination domains  
  - Bandwidth consumption  
  - Session upload/download volume  
  - Session duration  
- **Primary Threat Vector:** Unauthorized high-volume data exfiltration from an internal endpoint

---

## Incident Summary

A customer reported that their internet was “so slow they were basically offline.”  
Firewall telemetry showed that:

- One internal workstation  
- Uploading continuously  
- Maxing out the full upstream bandwidth  
- Uploading >100 GB in under 3 hours  
- Destination: Microsoft SharePoint cloud storage

After SharePoint uploads were blocked, the same endpoint attempted:

- SharePoint Web uploads  
- And later, raw TLS/SSL uploads (likely obscured data channels)

This strongly indicated **intentional data exfiltration**, likely from a compromised system or insider threat activity.

The behavior persisted across **multiple days**, confirming it was not accidental or a one-off sync job.

---

## Detection Method

The incident was detected using:

- Firewall bandwidth analysis  
- Per-device traffic breakdown  
- Application usage logs (App-ID)  
- Domain and service categorization  
- Session duration and volume analysis  
- Behavioral anomalies

### Key Indicators:

- **Single host consuming >95% of upstream bandwidth**
- **Massive outbound upload volume**
- **Uploads occurring outside normal business patterns**
- **Switching exfiltration methods after blocks were implemented**
- **Persistent, multi-day activity even after multiple takedowns**
