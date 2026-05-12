# 🔐 Internal Security Audit — Botium Toys

**Framework:** NIST Cybersecurity Framework (NIST CSF)  
**Audit Type:** Internal IT Security Audit  
**Date:** April 2026  
**Risk Score:** 8 / 10 (High)

---

## 📋 Project Overview

This project is a simulated internal security audit conducted for **Botium Toys**, a fictional small U.S. toy retailer with a growing e-commerce presence serving domestic and international customers.

The audit was completed as part of the **Google Cybersecurity Certificate** program and demonstrates core skills in:

- Security auditing methodology
- Risk identification and assessment
- Controls evaluation using the NIST CSF
- Regulatory compliance analysis (PCI DSS, GDPR, SOC)
- Security recommendations and prioritization

---

## 🎯 Audit Scope & Goals

**Scope:** The entire IT security program at Botium Toys — all assets, internal processes, and procedures.

**Goals:**
- Assess all IT-managed assets
- Complete a Controls & Compliance Checklist
- Identify gaps in the current security posture
- Recommend remediation steps to reduce risk and achieve compliance

---

## 🗂️ Assets Evaluated

- On-premises equipment and employee end-user devices
- E-commerce platform and storefront systems
- Accounting, database, telecommunications, and inventory management software
- Internal network and internet infrastructure
- Data retention and storage systems
- Legacy end-of-life systems requiring manual monitoring

---

## 🔍 Key Findings

### ❌ Critical Gaps

| Gap | Compliance Impact |
|---|---|
| No encryption for credit card data or PII | PCI DSS, GDPR |
| All employees have access to all internal data | PCI DSS, SOC |
| No least privilege or separation of duties | SOC, PCI DSS |
| No Intrusion Detection System (IDS) | NIST CSF – Detect |
| No disaster recovery plan or data backups | Business Continuity |
| Weak, unenforced password policy | PCI DSS |
| No centralized password management | PCI DSS |
| No formal legacy system maintenance schedule | Operational Risk |

### ✅ Controls Already in Place

| Control | Status |
|---|---|
| Firewall with defined security rules | ✅ Operational |
| Antivirus software | ✅ Installed & monitored |
| Physical locks on all facilities | ✅ In place |
| CCTV surveillance | ✅ Up-to-date |
| Fire detection and prevention | ✅ Functioning |
| Data integrity controls | ✅ Implemented |
| GDPR 72-hour breach notification plan | ✅ Established |
| Privacy policies (IT department) | ✅ Enforced |

---

## ✅ Controls & Compliance Checklist Summary

### Administrative Controls
| Control | In Place? |
|---|---|
| Least Privilege | ❌ No |
| Disaster Recovery Plans | ❌ No |
| Password Policies (strong) | ❌ No |
| Access Control Policies | ❌ No |
| Separation of Duties | ❌ No |

### Technical Controls
| Control | In Place? |
|---|---|
| Firewall | ✅ Yes |
| Intrusion Detection System (IDS) | ❌ No |
| Encryption | ❌ No |
| Backups | ❌ No |
| Antivirus Software | ✅ Yes |
| Data Integrity Controls | ✅ Yes |
| Centralized Password Management | ❌ No |

### Physical Controls
| Control | In Place? |
|---|---|
| Physical Locks | ✅ Yes |
| CCTV | ✅ Yes |
| Fire Detection & Prevention | ✅ Yes |

### PCI DSS Compliance
| Best Practice | Met? |
|---|---|
| Authorized access to cardholder data only | ❌ No |
| Secure storage, processing, transmission | ❌ No |
| Data encryption | ❌ No |
| Secure password management | ❌ No |

### GDPR Compliance
| Best Practice | Met? |
|---|---|
| E.U. customer data kept private/secure | ❌ No |
| 72-hour breach notification plan | ✅ Yes |
| Data classification and inventory | ❌ No |
| Privacy policies enforced | ✅ Yes |

### SOC Type 1 / Type 2 Compliance
| Best Practice | Met? |
|---|---|
| User access policies established | ❌ No |
| PII/SPII kept confidential | ❌ No |
| Data integrity maintained | ✅ Yes |
| Data accessible to authorized users only | ❌ No |

---

## 🛠️ Recommendations (Prioritized)

| Priority | Action | Framework / Regulation |
|---|---|---|
| 🔴 Critical | Implement encryption for all cardholder data and PII | PCI DSS, GDPR |
| 🔴 Critical | Apply least privilege and separation of duties | SOC, PCI DSS |
| 🔴 Critical | Create disaster recovery plan and automated backups | Business Continuity |
| 🟠 High | Deploy an Intrusion Detection System (IDS) | NIST CSF – Detect |
| 🟠 High | Implement centralized password management with enforcement | PCI DSS, SOC |
| 🟠 High | Conduct full asset inventory and classification | NIST CSF – Identify |
| 🟡 Medium | Establish legacy system maintenance schedule | Operational Risk |
| 🟡 Medium | Expand GDPR privacy policy training to all staff | GDPR |

---

## 📁 Files in This Repository

| File | Description |
|---|---|
| `Botium_Toys_Security_Audit.docx` | Full formatted audit report (Word document) |
| `README.md` | This file — project summary and findings |

---

## 🧠 Skills Demonstrated

- **NIST CSF** — Applied all five functions: Identify, Protect, Detect, Respond, Recover
- **Risk Assessment** — Evaluated asset risk and impact levels
- **Controls Analysis** — Administrative, technical, and physical controls evaluation
- **Compliance** — PCI DSS, GDPR, SOC Type 1/2 evaluation
- **Security Recommendations** — Prioritized remediation roadmap
- **Documentation** — Professional audit report creation

---

## 📜 Certificate Context

This project was completed as part of the **Google Cybersecurity Professional Certificate** on Coursera — a program covering network security, Linux, SQL, SIEM tools, threat analysis, and security auditing.

---

*This is a simulated audit using a fictional company for educational and portfolio purposes.*
