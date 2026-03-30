# 🛡️ EDR Alert Investigation Lab (SOC Analyst Simulation)

## 📌 Objective
Analyze multiple alerts within an Endpoint Detection & Response (EDR) platform to identify attacker behavior, validate automated security actions, and determine appropriate analyst responses.

---

## 🖥️ Environment
- Platform: TryHackMe (EDR Simulation)
- Tool: Simulated EDR Dashboard
- Scope: Multiple endpoints across an enterprise environment

---

## 🚨 Alert 1: Initial Access via Malicious Office Document
![Initial Access](screenshots/initial-access.png)

### Summary
A user opened a macro-enabled Word document (`invoice.docm`) which triggered a chain of events resulting in an attempted payload download from an external domain.

### Process Chain
![Process Chain](screenshots/process-chain.png)

WINWORD.EXE → CMD.EXE → cURL.EXE → install.exe

### Key Findings
- Malicious macro execution from Office document
- Command prompt spawned by Word (suspicious behavior)
- cURL used to download external payload
- File written to disk but not executed

### Indicators of Compromise (IOCs)
- File: `install.exe`
- Domain: `files-wetransfer.com`
- IP Address: `1.161.138.92`

### Response Actions (EDR Observed)
- Malicious file was automatically quarantined
- External domain and IP were blocked
- Activity was logged and flagged by the EDR

### Analyst Assessment
- Behavior is consistent with phishing-based initial access
- Automated containment actions were effective
- No execution of payload observed
- Recommend enforcing macro restrictions and user awareness training

---

## 🚨 Alert 2: Credential Dumping via LSASS Memory Access
![LSASS Dump](screenshots/lsass-dump.png)

### Summary
A suspicious executable (`syncsvc.exe`) accessed LSASS memory, indicating credential dumping activity on the host.

### Process Chain
![Process Chain](screenshots/process-chain.png)

explorer.exe → syncsvc.exe → lsass.exe

### Key Findings
- Unauthorized access to LSASS process memory
- Binary executed from temporary AppData directory
- Evidence of credential dumping behavior
- Persistence mechanism identified via registry key

### Indicators of Compromise (IOCs)
![IOCs](screenshots/iocs.png)

- File: `syncsvc.exe`
- Path: `C:\Users\haris.khan\AppData\Local\Temp\syncsvc.exe`
- Domain: `files-wetransfer.com`
- Registry Key: `HKCU\...\Run\syncsvc`

### Response Actions (EDR Observed)
- Malicious binary flagged and quarantined
- Outbound connection attempts blocked by firewall
- Registry persistence mechanism flagged

### Analyst Assessment
- Activity matches known credential dumping techniques (MITRE T1003)
- High severity threat due to potential credential compromise
- Recommend:
  - Immediate host isolation
  - Credential reset for affected user
  - Full endpoint investigation for lateral movement

---

## 🚨 Alert 3: Execution from AppData Directory
![AppData Execution](screenshots/appdata-execution.png)

### Summary
An executable (`UpdateAgent.exe`) was detected running from a user AppData directory, initially flagged due to unusual execution location.

### Key Findings
- Execution from non-standard directory (AppData)
- Internal network communication observed
- No malicious behavior identified

### Indicators of Compromise (IOCs)
- File: `UpdateAgent.exe`
- Path: `C:\Users\daniel.richards\AppData\Roaming\UpdateAgent.exe`
- IP Address: `10.10.20.5`

### Threat Intelligence Classification
**Known internal IT utility tool**

### Response Actions (EDR Observed)
- Activity logged as observed
- File marked safe by internal threat intelligence database
- No containment action taken

### Analyst Assessment
- Behavior initially suspicious but validated as legitimate
- Demonstrates the importance of distinguishing false positives
- No remediation required
- Recommend continued monitoring

---

## 🧠 MITRE ATT&CK Techniques Observed
- Initial Access (T1566 – Phishing)
- Command Execution
- Credential Dumping (T1003)
- Persistence via Registry

---

## 📊 Conclusion
This investigation demonstrates the ability to:

- Analyze and triage EDR alerts
- Trace process execution chains
- Identify and interpret indicators of compromise (IOCs)
- Validate automated security controls
- Differentiate between malicious and benign activity
- Provide appropriate incident response recommendations

---

## 🧠 Key Takeaway
Even when security tools perform automated actions, a SOC analyst must validate, interpret, and assess the activity to ensure accurate threat detection and response.

- Distinguish between malicious and benign activity  
- Recommend appropriate response actions
