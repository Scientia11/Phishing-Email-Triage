# Final Verdict

## Executive Summary

A comprehensive phishing investigation was conducted on an email with the subject **"Urgent: Verify Your Wallet to Prevent Suspension."** The investigation included analysis of the email headers, originating IP address, email body, and embedded URL.

Unlike traditional phishing emails that rely on spoofed domains and failed authentication checks, this email successfully passed **SPF, DKIM, and DMARC** because it was delivered through **Zendesk's legitimate email infrastructure**. However, authentication only confirms that the email originated from an authorized Zendesk tenant—it does not verify that the sender or the content is trustworthy.

The email employed several social engineering techniques, including urgency, fear of account suspension, and a request for wallet verification. Combined with the use of a shortened URL and the lack of identifiable branding, these indicators strongly suggest that the email was designed to deceive recipients into visiting an attacker-controlled verification page.

---

# Investigation Summary

## 1. Subject Analysis

**Subject:**

> **Urgent: Verify Your Wallet to Prevent Suspension**

The subject immediately attempts to create urgency by warning that the recipient's wallet may be suspended unless verification is completed.

This technique is commonly observed in phishing campaigns targeting cryptocurrency users, where attackers exploit fear of losing access to digital assets.

**Finding:**

* Urgency-based social engineering.
* Fear of account suspension.
* Credential verification lure.

---

## 2. Email Header Analysis

The email headers were examined to determine the authenticity of the sender and identify technical indicators.

### Sender Information

**From:**

```text
help@ohalyycp.zendesk.com
```

**Reply-To:**

```text
help+id1236162@ohalyycp.zendesk.com
```

The sender and Reply-To addresses belong to the same Zendesk tenant, indicating consistency within the email infrastructure.

Unlike many phishing emails, there was no mismatch between the From and Reply-To fields.

---

### Email Authentication

| Authentication | Result |
| -------------- | ------ |
| SPF            | Pass   |
| DKIM           | Pass   |
| DMARC          | Pass   |

All authentication mechanisms passed successfully, confirming that the email was legitimately sent through the authenticated Zendesk tenant.

However, authentication does not guarantee that the content of the email is legitimate.

---

### Message-ID

The Message-ID references Zendesk infrastructure, further confirming that the message originated from Zendesk's mail servers.

---

## 3. Originating IP Investigation

The originating IP address:

**188.172.137.10**

was investigated using WHOIS.

### WHOIS Findings

* Organization: Zendesk International Limited
* Location: Dublin, Ireland
* ASN: AS16509 (Amazon.com, Inc.)
* Resolved Hostname:
  `mta-out10.pod17.euw1.zdsys.com`

The originating infrastructure belongs to Zendesk and is hosted on Amazon Web Services (AWS).

This confirms that the email was sent through legitimate cloud infrastructure rather than a spoofed mail server.

---

## 4. Email Content Analysis

The email requested immediate wallet verification to avoid account suspension.

Several social engineering techniques were identified:

* Urgency
* Fear of financial loss
* Generic language
* Lack of personalization
* Suspicious call-to-action
* Minimal branding

The email failed to identify:

* The wallet provider
* The recipient
* A wallet address
* A customer reference
* Any account-specific information

Instead, it relied almost entirely on psychological pressure to encourage immediate action.

---

## 5. URL Analysis

The embedded hyperlink directed users to:

```text
https://scnv.io/mJnb
```

The shortened URL no longer redirects to an active page and instead returns:

> **404 Error**
>
> "Looks like you followed a broken or expired link."

The use of a shortened URL conceals the intended destination, making it more difficult for recipients to verify the legitimacy of the link before clicking.

Although the landing page is no longer available, phishing infrastructure is frequently removed after campaigns end or after providers disable malicious content.

The inactive destination does not eliminate the risk posed by the email.

---

# Correlation of Findings

Each stage of the investigation was evaluated independently before correlating the evidence.

| Investigation Area        | Result                               |
| ------------------------- | ------------------------------------ |
| Subject Analysis          | Suspicious                           |
| Header Analysis           | Authenticated Zendesk Infrastructure |
| SPF                       | Pass                                 |
| DKIM                      | Pass                                 |
| DMARC                     | Pass                                 |
| Sender Consistency        | Verified                             |
| WHOIS Investigation       | Legitimate Zendesk Infrastructure    |
| Email Content             | Highly Suspicious                    |
| Social Engineering        | Present                              |
| Account Suspension Threat | Present                              |
| Generic Messaging         | Present                              |
| URL Shortener             | Present                              |
| URL Destination           | 404 (Expired/Removed)                |

---

# Indicators of Compromise (IOCs)

### Domains

* ohalyycp.zendesk.com
* scnv.io

### IP Address

* 188.172.137.10

### Email Addresses

* [help@ohalyycp.zendesk.com](mailto:help@ohalyycp.zendesk.com)
* [help+id1236162@ohalyycp.zendesk.com](mailto:help+id1236162@ohalyycp.zendesk.com)

### Subject

* Urgent: Verify Your Wallet to Prevent Suspension

---

# MITRE ATT&CK Mapping

| Technique | Description                                                  |
| --------- | ------------------------------------------------------------ |
| T1566.002 | Phishing: Spearphishing Link                                 |
| T1204.001 | User Execution                                               |
| T1656     | Impersonation                                                |
| T1585     | Establish Accounts                                           |
| T1586     | Compromise Infrastructure (Use of legitimate cloud services) |

---

# Final Assessment

**Classification:** **High-Confidence Phishing**

Although the email was delivered through **legitimate Zendesk infrastructure** and successfully passed **SPF, DKIM, and DMARC** authentication, the overall investigation identified multiple indicators consistent with phishing. The subject line created urgency by threatening wallet suspension, while the email body relied on fear-based messaging, generic language, minimal branding, and a call to immediately verify the recipient's wallet. The embedded hyperlink used a shortened URL, obscuring its intended destination, and now resolves to a **404 Error**, suggesting that the underlying page has been removed or expired—a common occurrence with short-lived phishing infrastructure.

The investigation highlights an important principle in email security: **successful email authentication does not guarantee legitimacy**. Cloud-based services such as Zendesk can be abused by attackers to send authenticated phishing emails that bypass basic email security checks. Therefore, authentication results must always be evaluated alongside the sender's context, the email content, social engineering techniques, and embedded links.

Based on the totality of the evidence, the email is assessed as a **high-confidence phishing attempt** that likely sought to trick recipients into visiting a fraudulent wallet verification page and disclosing sensitive information. The email should be treated as malicious, quarantined, and blocked, and the associated domains and URLs should be monitored or added to organizational threat intelligence and email filtering systems.
