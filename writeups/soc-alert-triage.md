# 🛡️ SOC Alert Triage – Phishing Investigation

## 📌 Overview
Investigated phishing alerts in a simulated SOC environment using TryHackMe. The analysis focused on validating indicators, correlating activity, and determining whether the alert represented a true security threat.

---

## 🎯 Objective
Determine whether the alert was a true positive or false positive by analyzing email characteristics, embedded links, and related network activity.

---

## 🔍 Investigation Process

### 1. Email Analysis
- Reviewed sender address, subject line, and timestamps  
- Identified spoofed domains impersonating legitimate services  
- Observed urgency-based language commonly used in phishing attacks  

### 2. URL & Domain Analysis
- Extracted embedded URLs from email content  
- Compared domains against known legitimate services  
- Identified suspicious domains such as:
  - `amazon.biz` (spoofed domain vs legitimate `amazon.com`)  

### 3. Indicator Validation
- Analyzed domains and URLs for malicious characteristics  
- Identified inconsistencies in branding and domain structure  
- Confirmed patterns consistent with phishing infrastructure  

### 4. Network Activity Review
- Reviewed firewall logs for outbound connections  
- Identified attempted communication with malicious domains  
- Confirmed connections were blocked by security controls  

---

## 🚨 Key Findings

- Emails contained spoofed domains designed to mimic trusted brands  
- Embedded links redirected to malicious external domains  
- Firewall logs confirmed attempted connections to flagged infrastructure  
- Attack leveraged **social engineering techniques** (urgency, impersonation)  

---

## 🧠 MITRE ATT&CK Mapping

- **T1566 – Phishing (Initial Access)**  
- **T1204 – User Execution**  

---

## 📊 Analyst Assessment

- Classified as **True Positive (Phishing)**  
- Activity is consistent with credential harvesting or malware delivery attempts  
- Security controls successfully prevented compromise  

---

## 🛠️ Response Actions

- Blocked identified malicious domains  
- Documented phishing indicators for future detection  
- Confirmed no successful user interaction or system compromise  

---

## 🔐 Recommendations

- Strengthen email filtering for spoofed domains  
- Implement domain reputation checks for embedded links  
- Conduct user awareness training on phishing indicators  
- Monitor for repeated campaigns using similar infrastructure  

---

## 🧠 Analyst Decision

**Severity:** Medium  

**Verdict:** True Positive  

**Key Indicators:**  
- Spoofed domain (`amazon.biz`)  
- Social engineering language (urgency/impersonation)  
- Malicious external links  
- Blocked outbound connection attempts  

**Summary:**  
The alert was confirmed as a phishing attempt leveraging spoofed domains and social engineering techniques. Network controls prevented successful communication with malicious infrastructure, reducing the risk of compromise.

**Recommended Actions:**  
- Continue monitoring for similar phishing campaigns  
- Maintain domain blocking and filtering controls  
- Reinforce user awareness training  

---

## 📌 Conclusion

This investigation demonstrates the ability to:

- Validate phishing indicators and detect spoofed domains  
- Correlate email threats with network activity  
- Classify alerts based on evidence  
- Apply structured SOC triage methodology  
- Document findings and recommend appropriate response actions  

---

## 🧠 Key Takeaway

Effective phishing detection requires validating indicators, correlating activity across systems, and understanding attacker techniques to accurately assess risk and response.
