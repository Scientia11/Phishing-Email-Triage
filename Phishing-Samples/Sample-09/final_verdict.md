# Final Investigation Report

## Executive Summary

A comprehensive phishing investigation was conducted on an email claiming to be a **Norton subscription renewal confirmation**. The email informed the recipient that a two-year Norton subscription had been automatically renewed and that **$299.95** had been charged to their account. The recipient was instructed to call a provided telephone number if they did not recognize the transaction.

The investigation included analysis of the email headers, sender infrastructure, originating IP address, email content, and social engineering techniques. While the message successfully passed **SPF**, **DKIM**, and **DMARC** authentication, these validations applied only to the sender's **Gmail account** and not to the Norton brand being impersonated.

The overall findings indicate that the email is **not a legitimate Norton communication**, but rather a **telephone-oriented phishing campaign (TOAD)**, commonly referred to as a **refund scam**. Its primary objective is to persuade recipients to call a fraudulent support number, where attackers can conduct additional social engineering, request sensitive financial information, or convince victims to install remote access software.

---

# Investigation Summary

## 1. Subject Analysis

**Subject:**

> **Order Confirmation Alert**

The subject immediately creates concern by implying that a purchase has been completed. It is intentionally vague and lacks details such as an order number, customer name, or product information, encouraging recipients to open the email to verify the transaction.

**Findings**

* Generic financial-themed subject.
* Creates curiosity and concern.
* Consistent with refund scam campaigns.

---

## 2. Header Analysis

### Claimed Organization

The email claims to originate from **Norton**, a well-known cybersecurity software provider.

### Actual Sender

```text
From: monaschwartz732@gmail.com
```

Instead of an official Norton-owned domain, the sender uses a personal Gmail account.

This represents a significant mismatch between the claimed organization and the actual sender identity.

### Message-ID

```text
64ccabc0.0c0a0220.e604.27c8@mx.google.com
```

The Message-ID confirms that the message was transmitted through Google's mail infrastructure rather than Norton infrastructure.

### Return-Path

The Return-Path matches the Gmail sender address, indicating the email genuinely originated from that Gmail account rather than spoofing another address.

### Email Authentication

| Authentication | Result |
| -------------- | ------ |
| SPF            | Pass   |
| DKIM           | Pass   |
| DMARC          | Pass   |

Although all authentication mechanisms passed, they only verify that the message was legitimately sent from **gmail.com**. They do not establish any relationship between the sender and Norton.

**Header Assessment**

* Email genuinely originated from Gmail.
* No evidence connecting the sender to Norton.
* Strong indication of brand impersonation.

---

## 3. Originating IP Investigation

### Originating IP

```text
184.72.191.7
```

### WHOIS Findings

| Field         | Value                                    |
| ------------- | ---------------------------------------- |
| Location      | Dulles, Virginia, USA                    |
| Network Owner | Amazon Data Services                     |
| ASN           | AS14618 – Amazon.com, Inc.               |
| Hostname      | ec2-184-72-191-7.compute-1.amazonaws.com |

The IP address belongs to **Amazon Web Services (AWS)**, a legitimate cloud hosting provider.

While AWS is commonly used by legitimate organizations, it is equally available to attackers. There is no evidence that this infrastructure belongs to Norton.

**IP Assessment**

* Legitimate cloud provider.
* Infrastructure unrelated to Norton.
* Neutral individually, but suspicious when correlated with other findings.

---

## 4. Email Content Analysis

The email informs the recipient that:

* Their Norton subscription expired.
* A new two-year subscription has already been purchased.
* Their account has been charged **$299.95**.
* They should call **+1 (866) 955-9506** if they did not authorize the purchase.

### Social Engineering Indicators

The message contains numerous characteristics commonly associated with refund scams.

#### Generic Greeting

> Dear Member

No customer name or account information is provided.

#### Financial Lure

A significant charge of **$299.95** is used to provoke concern.

#### False Urgency

Recipients are encouraged to react immediately after learning of the alleged unauthorized charge.

#### Telephone Callback

Instead of directing users to their Norton account or official website, the email instructs recipients to call a support number.

This is characteristic of **Telephone-Oriented Attack Delivery (TOAD)** campaigns.

#### Fabricated Transaction Details

The email includes:

* Billing ID
* Activation key
* Renewal date
* Tax amount

These details appear legitimate but cannot be independently verified and are likely fabricated to increase credibility.

---

## 5. Social Engineering Assessment

The attacker attempts to manipulate the victim through several psychological techniques.

| Technique           | Purpose                                                    |
| ------------------- | ---------------------------------------------------------- |
| Brand Impersonation | Gain trust using the Norton name                           |
| Financial Fear      | Create panic over a large charge                           |
| Urgency             | Encourage immediate action                                 |
| Authority           | Present the email as an official invoice                   |
| Telephone Callback  | Move the victim into a live conversation with the attacker |

Unlike traditional phishing emails that direct victims to malicious websites, this campaign relies on convincing the recipient to initiate telephone contact.

---

# Indicators Identified

| Indicator                     | Status               |
| ----------------------------- | -------------------- |
| Brand Impersonation           | Detected             |
| Personal Gmail Sender         | Detected             |
| Generic Greeting              | Detected             |
| Fake Subscription Renewal     | Detected             |
| Fake Billing Information      | Detected             |
| High-Dollar Charge            | Detected             |
| Fear-Based Social Engineering | Detected             |
| Telephone Callback Scam       | Detected             |
| AWS Infrastructure            | Detected             |
| SPF Pass                      | Yes (gmail.com only) |
| DKIM Pass                     | Yes (gmail.com only) |
| DMARC Pass                    | Yes (gmail.com only) |

---

# Indicators of Compromise (IOCs)

## Email Address

```text
monaschwartz732@gmail.com
```

## Originating IP

```text
184.72.191.7
```

## Hostname

```text
ec2-184-72-191-7.compute-1.amazonaws.com
```

## Subject

```text
Order Confirmation Alert
```

## Telephone Number

```text
+1 (866) 955-9506
```

---

# MITRE ATT&CK Mapping

| Technique     | Description                                                                                    |
| ------------- | ---------------------------------------------------------------------------------------------- |
| **T1566.003** | Phishing: Spearphishing via Service (abuse of Gmail to deliver phishing content)               |
| **T1656**     | Impersonation (abusing the Norton brand to gain trust)                                         |
| **T1204**     | User Execution (persuading the victim to take an action, in this case calling the scam number) |

---

# Risk Assessment

| Category           | Rating                                |
| ------------------ | ------------------------------------- |
| Credential Theft   | Medium                                |
| Financial Fraud    | High                                  |
| Social Engineering | High                                  |
| Malware Delivery   | Low (no evidence in current analysis) |
| Overall Risk       | **High**                              |

---

# Final Assessment

**Classification:** **Confirmed Phishing / Refund Scam (TOAD Campaign)**

**Confidence Level:** **High**

The investigation concludes with high confidence that this email is a **fraudulent Norton subscription renewal scam**. Although the message successfully passed SPF, DKIM, and DMARC authentication, these mechanisms only verified the legitimacy of the **Gmail sender domain** and did not establish any association with Norton. The email originated from a personal Gmail account, with supporting infrastructure hosted on Amazon Web Services, neither of which are consistent with official Norton billing communications.

The content employs classic social engineering techniques by falsely claiming that a **$299.95** subscription renewal has already been processed. Rather than directing recipients to an official Norton portal, the email instructs them to call **+1 (866) 955-9506**, indicating that the attack is designed to transition victims into a live conversation with scammers. This behavior is characteristic of a **Telephone-Oriented Attack Delivery (TOAD)** or **refund scam**, where attackers attempt to obtain payment card information, online banking credentials, or convince victims to install remote access software under the guise of resolving the issue.

No evidence was found that the email originated from Norton infrastructure or that the transaction described in the message was legitimate. Based on the combined header analysis, infrastructure investigation, and content analysis, the email should be classified as **malicious**. Recipients should not call the provided phone number, disclose any personal or financial information, or treat the message as a genuine Norton billing notification. Any related indicators of compromise should be documented and, where appropriate, added to organizational email filtering and threat detection systems.
