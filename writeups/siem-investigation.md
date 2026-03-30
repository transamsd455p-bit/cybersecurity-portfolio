# SIEM Investigation: CryptoMiner Detection

## Overview
During routine SIEM monitoring, an alert was triggered indicating potential cryptomining activity on an endpoint. This investigation analyzes the alert, validates whether the activity is malicious, and determines the appropriate response.

---

## 1. SIEM Dashboard Analysis

![SIEM Dashboard](../screenshots/siem-dashboard.png)

Initial review of the SIEM dashboard revealed an anomalous process (`cudominer.exe`) not typically observed in baseline system activity. The process appeared alongside normal system processes, making it stand out as suspicious.

### Analyst Notes
- `cudominer.exe` is not a standard Windows process  
- Low execution count suggests recent or isolated activity  
- Likely introduced via user execution or a dropped payload  

---

## 2. Alert Triggered

![SIEM Alert](../screenshots/siem-alert.png)

The SIEM generated an alert for **Potential CryptoMiner Activity**, indicating a rule match based on suspicious process naming conventions.

### Analyst Interpretation
This alert suggests possible resource hijacking behavior, commonly associated with unauthorized cryptomining.

---

## 3. Event Investigation

![Event Logs](../screenshots/siem-event.png)

The investigation of event logs identified:

- **Host:** HR_02  
- **User:** Chris  
- **Process Path:** `C:\Users\Chris\temp\cudominer.exe`  

### Key Observations
- Execution from `Temp` directory → **highly suspicious**  
- User-level execution → possible phishing or malicious download  
- Process name includes “miner” → aligns with alert logic  

---

## 4. Detection Rule Analysis

![Detection Rule](../screenshots/siem-rule.png)

The alert was triggered based on:

- **Event ID:** 4688 (Process Creation)  
- **Rule logic:**  
  - Process name contains `miner` or `crypt`  

### Analyst Insight
This rule is effective for detecting known cryptomining indicators but may generate false positives if not tuned with additional context.

In this case, the process name directly matched known malicious patterns, increasing confidence in the alert.

---

## 5. IOC Analysis

### Identified Indicators of Compromise

- Process: `cudominer.exe`  
- File Path: `C:\Users\Chris\temp\`  
- Host: `HR_02`  
- Event ID: `4688`  

### Threat Context
Cryptominers are commonly:
- Delivered via phishing emails or malicious downloads  
- Executed from temporary directories  
- Designed to evade detection while consuming system resources  

---

## 6. MITRE ATT&CK Mapping

- **T1496 – Resource Hijacking**  
- **T1059 – Command Execution**  

### Explanation
The observed activity aligns with **Resource Hijacking**, where system resources are abused for unauthorized cryptocurrency mining.

---

## 7. Incident Response

![Response](../screenshots/siem-response.png)

The alert was classified as a **True Positive**, and the affected host was isolated.

### Analyst Decision
- Containment required due to confirmed malicious behavior  
- Isolation prevents further execution and potential lateral movement  
- Additional investigation recommended to determine initial access vector  

---

## 8. Recommendations

Based on the findings from this investigation, the following actions are recommended:

- **Implement application control / allowlisting**  
  Restrict unauthorized binaries from executing, especially from user directories such as `AppData` and `Temp`.

- **Enhance monitoring of temporary directories**  
  Configure SIEM alerts to flag process execution originating from `C:\Users\*\AppData\` and `Temp` paths.

- **Tune detection rules with additional context**  
  Improve existing rules by incorporating file path, parent process, and execution frequency to reduce false positives and improve detection accuracy.

- **Perform endpoint threat hunting**  
  Conduct a sweep across endpoints to identify similar indicators (e.g., `cudominer.exe` or similar process names).

- **User awareness and initial access review**  
  Investigate how the file was introduced (e.g., phishing, download) and reinforce user awareness training to prevent recurrence.

- **Strengthen endpoint protection controls**  
  Ensure EDR/AV solutions are configured to detect and block cryptomining behavior.

---

## Conclusion

This investigation confirmed unauthorized cryptomining activity on a corporate endpoint. The SIEM detection rule successfully identified the threat based on process naming patterns and execution behavior.

This scenario highlights:
- The importance of validating alerts  
- Recognizing suspicious execution paths  
- Applying structured analysis to determine impact and response  

By expanding beyond the alert and analyzing context, this investigation reflects real-world SOC workflows and demonstrates practical experience in threat detection and incident response.
