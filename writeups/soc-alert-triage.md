# 🛡️ SOC Alert Triage – Phishing Investigation

## 📌 Overview
Analyzed inbound phishing alerts in a simulated SOC environment using TryHackMe. The investigation focused on validating alerts, identifying malicious indicators, and determining whether activity represented a true security threat.

---

## 🎯 Objective
Determine whether alerts were true positives or false positives by analyzing email characteristics, embedded links, and supporting network activity.

---

## 🔍 Investigation Process

### 1. Email Analysis
- Reviewed sender address, subject line, and timestamps  
- Identified spoofed domains attempting to impersonate legitimate services  
- Observed urgency-based language commonly used in phishing attacks  

### 2. URL & Domain Analysis
- Extracted embedded URLs from email content  
- Compared domains against known legitimate services  
- Identified suspicious domains such as:
  - `amazon.biz` (spoofed domain vs legitimate `amazon.com`)  

### 3. Indicator Validation
- Checked domains and URLs for malicious characteristics  
- Observed patterns consistent with phishing infrastructure  
- Identified mismatched branding and domain structure  

### 4. Network Activity Review
- Analyzed firewall logs for outbound connections  
- Confirmed attempted communication with flagged domains  
- Verified that connections were blocked by security controls  

---

## 🚨 Key Findings

- Emails contained spoofed domains designed to mimic trusted brands  
- Embedded links redirected to non-legitimate external domains  
- Firewall logs confirmed attempted access to malicious infrastructure  
- Attack leveraged **social engineering techniques** (urgency, impersonation)  

---

## 🧠 MITRE ATT&CK Mapping

- **T1566 – Phishing (Initial Access)**  
- **T1204 – User Execution**  

---

## 📊 Analyst Assessment

- Classified as **True Positive (Phishing)**  
- Attack represents a typical phishing attempt aimed at credential harvesting or malware delivery  
- Security controls (firewall + filtering) successfully prevented user compromise  

---

## 🛠️ Response Actions

- Blocked identified malicious domains  
- Logged and documented phishing indicators  
- Confirmed no successful user interaction or compromise  

---

## 🔐 Recommendations

- Implement stricter email filtering for spoofed domains  
- Enforce domain reputation checks on embedded links  
- Conduct user awareness training focused on phishing indicators  
- Monitor for repeated phishing campaigns using similar infrastructure  

---

## 📌 Conclusion

This investigation demonstrates the ability to:

- Analyze phishing alerts and validate indicators of compromise  
- Differentiate between legitimate and malicious domains  
- Correlate email-based threats with network activity  
- Apply structured SOC triage methodology  
- Document findings and recommend appropriate mitigation steps  

---

## 🧠 Key Takeaway

Effective phishing detection requires more than identifying suspicious emails—it involves validating indicators, correlating activity across systems, and understanding attacker techniques to determine real risk and appropriate response.
