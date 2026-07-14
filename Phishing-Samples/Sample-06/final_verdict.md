
# Final Verdict

## Executive Summary

The investigated email was assessed as a **high-confidence phishing email** designed to impersonate Microsoft and deceive recipients into believing that their Microsoft account had experienced unusual sign-in activity. The attack employed multiple social engineering techniques, deceptive email infrastructure, and misleading hyperlinks to manipulate the recipient into interacting with attacker-controlled communication channels.

A comprehensive analysis was conducted on the email subject, headers, body content, embedded links, and originating IP address. Individually, each component contained suspicious characteristics; collectively, they provided overwhelming evidence that the email was malicious.

---

# Investigation Summary

## Subject Line Analysis

**Subject:** *Microsoft account unusual signin activity*

The subject line was crafted to imitate a legitimate Microsoft security notification. By claiming unusual sign-in activity, the attacker attempted to create fear and urgency, encouraging the recipient to act immediately without verifying the authenticity of the email.

**Finding:**

* Security alert used as a phishing lure.
* Designed to trigger an emotional response and immediate action.

---

## Email Header Analysis

The email headers revealed numerous anomalies inconsistent with legitimate Microsoft communications.

### Sender Domain

**From:**

```
no-reply@access-accsecurity.com
```

The sender domain is unrelated to Microsoft's official infrastructure, indicating brand impersonation.

---

### Reply-To Address

```
solutionteamrecognizd03@gmail.com
```

Instead of directing responses to Microsoft, all replies were redirected to a personal Gmail account controlled by the attacker.

---

### Return-Path

```
bounce@atujpdfghher.co.uk
```

The Return-Path used an entirely different domain from both the sender and Reply-To addresses.

The presence of three unrelated domains within a single email is highly suspicious and inconsistent with legitimate enterprise email infrastructure.

---

### Email Authentication

| Authentication | Result |
| -------------- | ------ |
| SPF            | None   |
| DKIM           | None   |
| DMARC          | None   |

The absence of all three authentication mechanisms significantly reduces trust in the sender and indicates that the domain lacks protections commonly implemented by legitimate organizations.

---

## Originating IP Investigation

The originating IP address:

```
89.144.44.49
```

was investigated using WHOIS.

The lookup revealed:

* Location: Germany
* Network Owner: MSCode.pl
* ASN: AS201132
* Abuse Contact Available

The infrastructure is unrelated to Microsoft.

Although IP ownership alone does not confirm malicious activity, when correlated with the remaining evidence it further supports the phishing assessment.

---

## Email Content Analysis

The email claimed that an unusual login had occurred from:

* Russia (Moscow)
* Windows 10
* Firefox browser

The attacker included technical information to increase the credibility of the notification.

The email instructed recipients to click a **"Report The User"** button if they did not recognize the login.

Several social engineering techniques were identified:

* Fear of account compromise
* Urgency
* Brand impersonation
* False legitimacy through fabricated login details
* Immediate call-to-action

---

## Embedded Link Analysis

The investigation revealed that both embedded hyperlinks:

* **Report The User**
* **Click here**

did not direct users to Microsoft.

Instead, both links resolved to:

```
mailto:solutionteamrecognizd03@gmail.com
```

This is a significant phishing indicator.

Rather than directing victims to Microsoft's official account recovery or security portal, the attacker attempted to establish direct communication through a personal Gmail account.

This technique could facilitate:

* Credential harvesting
* Collection of sensitive information
* Follow-up social engineering attacks

The embedded links also matched the Reply-To address found within the email headers, demonstrating a consistent attacker-controlled communication channel.

---

# Correlation of Findings

Every stage of the investigation supported the phishing assessment.

| Investigation Area  | Result                                |
| ------------------- | ------------------------------------- |
| Subject Analysis    | Suspicious                            |
| Header Analysis     | Malicious Indicators Found            |
| Sender Domain       | Impersonation                         |
| Reply-To Address    | Gmail Account                         |
| Return-Path         | Unrelated Domain                      |
| SPF                 | Missing                               |
| DKIM                | Missing                               |
| DMARC               | Missing                               |
| WHOIS Investigation | Infrastructure Unrelated to Microsoft |
| Email Content       | Social Engineering                    |
| Embedded Links      | Redirect to Attacker Gmail            |
| Overall Risk        | High                                  |

---

# Indicators of Compromise (IOCs)

### Domains

* access-accsecurity.com
* atujpdfghher.co.uk

### Email Address

* [solutionteamrecognizd03@gmail.com](mailto:solutionteamrecognizd03@gmail.com)

### Originating IP

* 89.144.44.49

### Subject

* Microsoft account unusual signin activity

---

# MITRE ATT&CK Mapping

| Technique | Description                   |
| --------- | ----------------------------- |
| T1566.002 | Phishing: Spearphishing Link  |
| T1656     | Impersonation                 |
| T1204.001 | User Execution                |
| T1585     | Establish Accounts or Domains |
| T1586     | Compromise Infrastructure     |

---

# Final Assessment

Based on the evidence collected during this investigation, the email is classified as a **High-Confidence Phishing** attempt.

The attacker impersonated Microsoft and used a fabricated security alert regarding unusual sign-in activity to create urgency and manipulate the recipient into taking action. Technical analysis identified multiple inconsistencies, including an unrelated sender domain, a Gmail Reply-To address, a mismatched Return-Path, the absence of SPF, DKIM, and DMARC authentication, and hosting infrastructure unrelated to Microsoft. Furthermore, analysis of the embedded hyperlinks revealed that both the **"Report The User"** button and the **"click here"** link directed users to an attacker-controlled Gmail address instead of Microsoft's official security portal.

The convergence of these findings demonstrates a coordinated phishing campaign intended to deceive users and facilitate credential theft or further social engineering. The email should be classified as malicious, quarantined, and blocked from delivery. Additionally, the identified domains, email address, and originating IP should be added to threat intelligence and email filtering systems, and affected users should be advised not to interact with the message or provide any sensitive information.
